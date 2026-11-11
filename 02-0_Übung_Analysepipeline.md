# Übung Entwicklung einer Analysepipeline
*11.11.2026*

**Ziele:**
1. Methodik des Papers verstehen/Pipeline logisch zusammenfassen
2. Verständnis für die Nutzung von öffentliche klinische Daten 
3. Python Packages für Datenanalysen kennen
4. Datenaufbereitung mit Python
5. Bau einer Analysepipeline mit Python

## Recap 28.10.2026
1. Fragen zum letzten Mal?
2. Läuft Jupyter noch bei jeder Person?

## Part I: Die heutige Grundlage 

### Hypoxie
**Potenzial der Vorhersage von Hypoxie mittels ML:**
- individuelle Vorhersage innerhalb einer bestimmten Zeit
- Möglichkeit vor akuter Zustandsverschlechterung zu warnen (Intensivstation)
-> verbesserte Versorgung + effizientere Ressourcennutzung

**Möglichkeiten**:
- Vorhersageergebnis: Zeitrahmen (1, 5, 30 min?), binäre, Schweregrad
- Definition: einfachste Lösung: Hypoxämie -> Schwellenwerte?
- Parameter: Patientencharakteristika, vorherige $SpO_2$ Werte
- ML-Modelle: konventionelle Modelle (Regression, k-nearest neighbors), neuronale Netze

### Das SWIFT Modell
_$SpO_2$ Waveform ICU Forecasting Technique_

[Annapragada et al. (2021) SWIFT: A deep learning approach to prediction of hypoxemic events in critically-Ill patients using SpO2 waveform prediction. PLoS Comput Biol 17(12)](https://doi.org/10.1371/journal.pcbi.1009712)

-> 30-40 min

Fragen:
1. Was ist das grundsätzliche Ziel des Modells
2. Welche Patienten oder Datenbanken werden verwendet?
3. Wie wird Hypoxämie definiert?
4. Welche Inputvariable(n) wird/werden verwendet?
5. Welche ML-Algorithmen werden verwendet?
6. Weitere (nicht genannte) Limitationen des Papers
7. Grafische Darstellung der Pipeline

> Ziel 1 erfüllt.

## Part II: öffentliche Datensets

Fragen: 
- Welche Herausforderungen gibt es, um Datensätze öffentlich verfügbar zu machen?
- Welche öffentlichen Datenbanken mit Gesundheitsdaten kennt ihr?

### MIMIC-IV Datenbank
- [Medical Information Mart for Intensive Care (MIMIC)-IV](https://physionet.org/content/mimiciv/3.1/), a large deidentified dataset of patients admitted to the emergency department or an intensive care unit at the Beth Israel Deaconess Medical Center in Boston, MA
- MIMIC-IV contains data for over **65,000** patients admitted to an **ICU** and over **200,000** patients admitted to the **emergency** **department** (2008 - 2022).

**Access Policy**:
Only credentialed users who sign the [DUA](https://physionet.org/content/mimiciv/view-dua/3.1/) can access the files.
**Required Training**:
[CITI Data or Specimens Only Research](https://physionet.org/content/mimiciv/view-required-training/3.1/#1)
**Website**:
[Official Website](https://mimic.mit.edu/)

**Database Demo**: 
[https://physionet.org/content/mimic-iv-demo/2.2/](https://physionet.org/content/mimic-iv-demo/2.2/ "https://physionet.org/content/mimic-iv-demo/2.2/")

### Weitere öffentliche Datensätze mit Patientendaten
- UC Berkeley Library führt eine große Übersicht zu [Health Statistics & Data: Datasets/Raw Data](https://guides.lib.berkeley.edu/publichealth/healthstatistics/rawdata)
- Übersicht aus Medium: [18 Open Healthcare Datasets — 2025 Update](https://odsc.medium.com/18-open-healthcare-datasets-2025-update-935cbfe0a497)

> Ziel 2 erfüllt.

## Part III: Python Packages 

- [numpy](https://numpy.org/): [Übungsnotebook](02-1_NumPy_Tutorial.ipynb)
- [pandas](https://pandas.pydata.org/): [Übungsnotebook](02-2_Pandas_Tutorial.ipynb)
- [matplotlib](https://matplotlib.org/)*: [Übungsnotebook](02-3_Matplotlib_Tutorial.ipynb)
- [scikit-learn](http://scikit-learn.org/): [Übungsnotebook](02-4_scikit-learn_Tutorial.ipynb)

\**Matplotlib wurde bereits in dem Beispielnotebook aus der letzten Session verwendet.*

Installtation mit:
```
    # aktiviere die virtuelle Umgebung

    # MacOS
    source <venv>/bin/activate

    # Windows
    <venv>\Scripts\activate 
    # oder 
    <venv>\Scripts\Activate.ps1

    # Installation
    pip install numpy pandas matplotlib scikit-learn
```

> Ziel 3 erfüllt.

## Part IV: Hands-on

Dies ist der größte Part. Er umfasst neben des heutigen Termins (11.11.) auch die Online-Übung.

![alt text](<.images/Pasted image 20261109134108.png>)

### 1. Fragestellung
Wie lautet die Fragestellung, dir wir mit den MIMIC-IV Daten beantworten wollen?

### 2. Daten
Was ist unser Patientenkollektiv/welche Daten verwenden wir?

### 3. Aufbereitung
Oft auch Preprocessing genannt.

-> Notebook [Datenaufbereitung](02-5_Datenaufbereitung_SpO2_Uebung.ipynb)

> Ziel 4 erfüllt.

### 4. Modell
Übung bis zum 18.11.2026

-> Notebook [Modellentwicklung](02-6_Modellentwicklung_SpO2_Uebung.ipynb)

> Ziel 5 erfüllt.
