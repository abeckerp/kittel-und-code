# Besprechung der Analysepipeline
*18.11.2026*

**Ziele:**

## 5. Evaluation

### Warum das Modell hier Sinn macht – und wo nicht

**Als Methode ist der Random Forest eine gute Wahl.**

- Durch das Schiebefenster wird aus der Zeitreihe eine normale Tabelle.
- Der Random Forest erkennt nichtlineare Muster wie Trends oder Ausreißer, ohne dass man Merkmale selbst konstruieren muss.
- Er braucht keine Standardisierung und ist durch das Mitteln vieler Bäume robust.
- Er sagt immer Mittelwerte aus echten Trainingswerten vorher. Deshalb gibt er nie unmögliche Werte wie 103 % aus.
- Bei 13.000 Zeilen ist er in Sekunden trainiert. Für ein neuronales Netz wäre der Datensatz zu klein.

**Ehrlich gesagt** schneidet er aber auf diesem Datensatz kaum besser ab als triviale Regeln. Ich habe das Teil 2 der Lösung bewusst zum Kern gemacht, denn daraus ergibt sich die eigentliche Lektion:

|Befund|Zahlen|
|---|---|
|Random Forest mit Standardeinstellungen|MAE 1,47, R² 0,28|
|Regel „Mittelwert der letzten 5 Werte“|MAE 1,41, R² 0,33, also **besser**|
|Random Forest mit `min_samples_leaf=20`|schlägt die Baseline, aber knapp|
|Erkennung von Entsättigungen < 92 %|Random Forest 17 %, einfache Regeln ca. 35 %|

Der Grund: SpO₂-Schwankungen sind größtenteils Messrauschen. Die Abweichungen bewegen sich im Bereich der Pulsoxymeter-Genauigkeit von etwa ±2 %. Das zeigt den Studierenden mehrere Dinge:

- Man braucht immer eine Baseline.
- Standardeinstellungen führen bei verrauschten Daten zu Overfitting.
- Ein besserer MAE bedeutet nicht automatisch einen besseren klinischen Nutzen.
- Die Grenze liegt in den Daten, nicht im Algorithmus.

Dazu passt auch Tutorial 04 (Sensitivität, Schwellenwerte).
### Vorschlag für die 2 Stunden

|Zeit|Inhalt|
|---|---|
|0–40 min|Teil 1 besprechen: `create_sequences` mit Funktionstest am Mini-Beispiel, Training, Gütemaße, die beiden Grafiken. Erste Auffälligkeit: Overfitting (R² Training 0,81 gegenüber Test 0,28).|
|40–55 min|2.1 Baseline. Lassen Sie die Studierenden vorher raten, ob das Modell besser ist.|
|55–70 min|2.2 Aufteilung nach Patient*innen (Datenleck). Gut zu wissen: In diesem Datensatz ist der Effekt klein, im Notebook ist das ehrlich erklärt.|
|70–85 min|2.3–2.6 Hyperparameter, Sequenzlänge, Feature Importance|
|85–100 min|2.7 Verlaufsgrafik („das Modell hinkt hinterher“) und 2.8 Entsättigungen, Alarmgrenze, Alarm Fatigue|
|100–120 min|Fazit und vier Diskussionsfragen (weitere Vitalparameter, Zeitabstände, besseres Ziel, Übertragbarkeit)|

Die drei Zellen mit Kreuzvalidierung brauchen jeweils etwa eine halbe bis eine Minute. Am besten führen Sie das Lösungsnotebook vor der Stunde einmal komplett aus.


**Evaluation**

- **3.1 Bootstrap-Konfidenzintervall**, wobei Patient*innen gezogen werden und nicht einzelne Sequenzen. Das Notebook begründet, warum.
    - Ergebnis: Der Random Forest ist 0,056 Prozentpunkte besser als die Baseline, 95-%-KI [0,008; 0,089].
    - Botschaft: Der Unterschied ist statistisch nachweisbar, aber klinisch irrelevant.
- **3.2 Bland-Altman-Plot**, den die Studierenden aus dem Methodenvergleich kennen.
    - Der Bias ist praktisch 0, die Limits of Agreement liegen bei etwa ±4 Prozentpunkten.
    - Die Fehler des Modells sind etwa so groß wie die Messungenauigkeit eines Pulsoxymeters selbst.
    - Bei niedrigen Werten überschätzt das Modell den SpO₂ aber systematisch, also in der gefährlichen Richtung.
- **3.3 Fehler pro Person.** Der Random Forest ist nur bei 13 von 20 Personen besser als die Baseline. Der MAE reicht von 0,5 bis 3,4 Prozentpunkten.
- **3.4 Fehler nach Zeitabstand.** Liegen mehr als 60 Minuten bis zur nächsten Messung, steigt der Fehler deutlich. Das ist ein konkreter Ansatz, um das Modell zu verbessern.
- 
## 6. Interpretation 
- **3.5 Permutation Importance** auf den Testdaten, als robustere Ergänzung zur eingebauten Feature Importance. Die letzte Messung trägt etwa 40 % des Fehlers.
- **3.6 Partial-Dependence-Plot** für den letzten Wert. Er zeigt die Regression zur Mitte, dass das Modell nicht extrapolieren kann, und Sprünge ohne physiologische Logik in Bereichen mit wenigen Daten.
- **3.7 Was-wäre-wenn-Szenarien:** Das Modell bekommt sechs typische klinische Verläufe vorgelegt, wie bei einer kleinen Fallbesprechung. Das wichtigste Ergebnis: Bei einem kontinuierlichen Abfall von 98 auf 90 % sagt das Modell 94 % voraus. Es schreibt Trends also nicht fort. Daran lässt sich das _treatment paradox_ gut erklären: Abfälle werden in den Daten meist behandelt, deshalb „lernt“ das Modell, dass sie harmlos sind.
- **3.8 Steckbrief des Modells** im Stil einer Model Card. Er eignet sich als Abschlussfolie.

## 7. Bericht
