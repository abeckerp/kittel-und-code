## Fragen:

1. Was ist das grundsätzliche Ziel des Modells

<detail>

<summary>Lösung anzeigen</summary>

Vorhersage des Auftretens und der Intensität von Hypoxämie 5 und 30 Minuten in die Zukunft
</detail>

2. Welche Patienten oder Datenbanken werden verwendet?

<detail>

<summary>Lösung anzeigen</summary>

2 Datenbanken: eICU-CRD und JH-CROWN (Covid-19-Patienten)
</detail>

3. Wie wird Hypoxämie definiert?

<detail>

<summary>Lösung anzeigen</summary>

$SpO_2$ < 92%
</detail>

4. Welche Inputvariable(n) wird/werden verwendet?

<detail>

<summary>Lösung anzeigen</summary>

Bisherige Sauerstoffsättigung ($SpO_2$)
</detail>

5. Welche ML-Algorithmen werden verwendet?

<detail>

<summary>Lösung anzeigen</summary>

Long short-term memory (LSTM) Modell basierend jeweils auf den zwei vorangehenden Messwerten
</detail>

6. Weitere (nicht genannte) Limitationen des Papers

<detail>

<summary>Lösung anzeigen</summary>

Fokus auf ältere Population; Möglicher Bias aufgrund der Ethnie; Gute Spezifität, aber mäßige Sensitivität; Aussagekraft durch kleine Zahl von True Positives reduziert; Schlechtere Performance bei Covid19-Patienten
</detail>

7. Grafische Darstellung der Pipeline

<detail>

<summary>Lösung anzeigen</summary>

![alt text](<.images/Pasted image 20261109130918.png>)

**Plot 1**

Title: SWIFT data preparation pipeline

Description: Flow from the eICU and JH-CROWN databases through cohort selection, interpolation, exclusion, transform and smoothing, resampling, and windowing into input/output pairs.


**Part 2: Model training and evaluation.** Training uses only non-COVID eICU patients; the COVID-19 cohort serves purely as an external test of generalization.

![alt text](<.images/Pasted image 20261109131024.png>)

**Plot 2**

Title: SWIFT model training and evaluation pipeline

Description: Training set feeds 3-fold cross-validation, architecture selection, and retraining, producing SWIFT-5 and SWIFT-30, which predict on three held-out test sets and are evaluated on waveform accuracy and hypoxemia classification.

Ein paar weitere Details:

**Weshalb wurden beatmete und nicht-beatmete Patienten separat getestet?**
Die Autoren haben einen chi-squared test durchgeführt, der zeigte, dass Beatmung signifikant mit der Anzahl der hypoxämen Zeitpunkten zusammenhing. Dies führte dazu, dass eICU Aufenthalte mit Beatmung als separates Testset für Aufenthalte ohne Beatmung verwendet wurden.

**Weshlab wurden $SpO_2$ Werte transformiert und geglättet?**
Da die $SpO_2$ Werte alle sehr schief waren (nah an 100%) wurden sie transformiert, um in diesem Bereich einen größeren Abstand zwischen den Werten zu erhalten. 
(The moving-average filter is causal, so it can be applied in real time, and it reduces transient noise. )

**Wie wurde der Hypoxemia-THreshold Wert angewandt?**
Das Modell hat kein ja/nein output label. Es berechnet einen $SpO_2$ Wert, und jeder Zeitpunkt - egal ob gemessen oder berechnet - wird gegen die 92% Threshold geprüft um Sensitivität, Spezifität, Accuracy and PPV für jeden AUfenthalt zu berechnen.

**Ergebnisse** 
Über alle Zeiträume hinweg hat der SWIFT Algorithmus mehr als 80% der hypoxämischen Events mit einem PPV von mehr als 94% in dieser kritisch kranken Kohorte berechnen können. In der COVID-19 Kohort wurden mehr als 60% identifiziert - bei einem PPV von mehr als 98%. Die Berechnung der Wellenform hat einen durchscnittlichen MSW von weniger als 0.0007 mit einem Pearson Korrelationsindex von über 0.95.
</detail>