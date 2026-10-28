# Einführung - Einrichtung der Laptops

*28.10.2026*

**Ziele**:
1. Python 3.1* ist auf dem Laptop installiert
2. Visual Studio Code ist installiert
3. Jupyter Notebooks ist installiert
4. optional/Hausaufgabe:
	  - Windows User: WSL ist installiert
	  - OpenCode ist installiert

# Part I
## Installation von Python
>Python ist eine Programmiersprache. Neben Applikationsentwicklungen eignet sie sich hervorragend für Datenauswertungen. Diese Vorlesungsreihe nutzt Python für die Datenanalysen.

Installation erfolgt über die offizielle [Python Webseite](https://python.org/). 
### Windows
#### Option 1 (bevorzugte Variante)
Auf der Downloadseite die passende Version herunterladen und installieren. Dabei darauf achten, dass das Häkchen zwingend bei "Add Python to PATH" gesetzt wird.
#### Option 2
Alternativ kann Python über den Microsoft Store oder den Paketmanager `winget install Python.Python.3` installiert werden. 
### MacOS
Hier ist Python in der Regel bereits vorinstalliert. Überprüfen mit `python3 --version`.
Sollte eine Installation fehlen kann auf zwei Wege Python installiert werden:
#### Option 1 (bevorzugte Variante)
Auf der Downloadseite den macOS installer herunterladen und die `.pkg`-Datei ausführen. Anweisungen des Installationsasisstenten sind zu befolgen.
#### Option 2
Alternativ kann Python über den Paketmanager Homebrew mit `homebrew install python3` installiert werden. 
### Linux 
Hier ist Python in der Regel bereits vorinstalliert. Überprüfen mit `python3 --version`.
Sollte eine Installation fehlen, wird sie je nach Distribution unterschiedlich installiert:
- **Ubuntu/Debian**: `sudo apt update && sudo apt install python3`
- **Fedora**: `sudo dnf install python3`
- **openSUSE**: `sudo zypper install python3`


>**Ziel 1: erfüllt**
## Installation von VS Code
>Visual Studio Code ist ein kostenloser Code-Editor von Microsoft, der für Windows, MacOS und Linux verfügbar ist. Wir verwenden ihn, um Jupyter Notebooks auszuführen, in denen die Datenanalysen geschrieben sind.

Der Download erfolgt ausschließlich über die offizielle Webseite von [VS Code](https://code.visualstudio.com/download).
### Windows
*https://code.visualstudio.com/docs/setup/windows*
Installation des [**User setup**](https://go.microsoft.com/fwlink/?LinkID=534107). Die Datei wird heruntergeladen, ausgeführt, die Lizenzvereinbarung wird akzeptiert und auch hier muss die Option "zum PATH hinzufügen" ausgewählt werden.
### MacOS
*https://code.visualstudio.com/docs/setup/mac*
[Download der](https://go.microsoft.com/fwlink/?LinkID=534106) `.dmg` Datei, diese muss im Anschluss in den Programm Ordner gezogen werden. 
### Linux
*https://code.visualstudio.com/docs/setup/linux*
Bitte der Anleitung für die jeweilige Distribution folgen.


**Im Anschluss an die Installation VS Code bitte öffnen.**
![alt text](<.images/Pasted image 20261027101945.png>)



Über die Auswahl des **Explorers** oben links wird nun ein Ordner ausgewählt (ggf. erstellt), in dem die Übungen und Projekte der Vorlesungsreihe gespeichert werden sollen (*Empfehlung: Benutzerverzeichnis, dort den Ordner "Kittel-und-Code" erstellen*). 
Dazu wählt man **Open Folder**:
![alt text](<.images/Pasted image 20261027102310.png>)

Im Anschluss wird ein Terminal geöffnet:
![alt text](<.images/Pasted image 20261027102652.png>)


Im Terminal wird die Installation von Python überprüft: `python3 --version`
Die Anzeige sollte ähnlich sein: `Python 3.14.4`. 

>**Ziel 2: erfüllt**

## Praktische Erweiterungen in VS Code
In VS Code können Erweiterungen installiert werden, die das Arbeiten vereinfachen. Dazu wird links in der Seitenleiste "Erweiterungen" ausgewählt:

![alt text](<.images/Pasted image 20261027132605.png>)

Folgende Erweiterungen sind hilfreich und empfehle ich zu installieren:
- Jupyter
- Python
- Rainbow CSV
- Todo Tree
## Virtuelle Umgebung erstellen
> Virtuelle Umgebungen sind in sich abgeschlossene Bereiche, in denen unterschiedliche Pakete installiert werden können, ohne mit anderen Umgebungen oder dem Betriebssystem in Konflikt zu geraten.
> ![alt text](<.images/Pasted image 20261027104234.png>)
>*Source: Claude*

**Erstellen**
	*Unter Umständen muss das Paket venv noch installiert werden (`pip install venv`)*
Um eine virtuelle Umgebung in dem Projektordner `Kittel-und-Code` zu erstellen, wird dort der Befehl `python -m venv .kuc-env` ausgeführt. In diesem Fall ist `.kuc-env` der Name für die virtuelle Umgebung, dieser kann aber frei gewählt werden (z.B. einfach `.venv`). *(Bei Ordnern oder Dateien mit einem führenden `.` handelt es sich um versteckte Dateien.)*

**Aktivieren**
Die virtuelle Umgebung muss zu Beginn einer jeden Session gestartet werden, da ansonsten installierte Packages nicht geladen werden. Unter Windows wird die virtuelle Umgebung über `.kuc-env\Scripts\activate` gestartet, unter MacOS oder Unix mit `source .kuc/bin/activate`. 

**Installieren**
Nun können beliebige Pakete installiert werden (`pip install <package>`), die für wissenschaftliche Datenauswertungen benötigt werden. Die bekanntesten und am meisten verbreiteten Pakete sind pandas, numpy, scikit learn, matplotlib und seaborn. Die beiden letzten werden zur Visualisierung genutzt. 
Eine kleine (bereits etwas ältere) Übersicht findet sich bei [Analytics Vidhya](https://www.analyticsvidhya.com/blog/2021/02/key-python-packages-for-data-science/)*(Analytics Vidhya is a community of Generative AI and Data Science professionals)*. 

## Installation von Jupyter Notebooks
>Jupyter Notebooks sind ein Produkt des [Projekts Jupyter](https://jupyter.org/). Mit ihnen können interaktive wissenschaftliche Datenauswertungen und Berechnungen vorgenommen werden. Sie unterstützen die Sprachen Python, R und Julia.
![alt text](<.images/Pasted image 20261027101546.png>)

*Source: [Jupyter](https://jupyter.org/assets/homepage/jupyterpreview.webp)*

Die klassische Installation erfolgt über den Paketmanager `pip` in Python, der Befehl wird direkt im Terminal ausgeführt (in der aktivieren virtuellen Umgebung):
`pip install jupyter`

## Verwendung von Jupyter Notebooks
> Jupyter Notebooks haben immer die Dateiendung `.ipynb`. Sie bestehenden aus verschiedenen ausführbaren Zellen, die entweder Python Code oder Markdown beinhalten. Bei [Markdown](https://www.markdownguide.org/basic-syntax/#overview) handelt es sich um eine vereinfachte Auszeichnungssprache mit HTML-Preview.

In VS Code können entweder über `Datei > neue Datei` oder über das Symbol im Explorer neue Dateien erstellt werden. Die virtuelle Umgebung wird in der Regel automatisch erkannt und geladen. Sie kann aber auch manuell ausgewählt werden (ggf. muss sie im Terminal einmal aktiviert werden). 

In einer Datei können beliebig viele Markdown und Python Cells von beliebiger länger verwendet werden. Dies kann so aussehen:
![alt text](<.images/Pasted image 20261027113641.png>)


Über `Run All` können nun alle Zellen nacheinander mit nur einem Klick ausgeführt werden. Alternativ kann jede Zelle einzeln ausgeführt werden; so können Codeänderungen direkt überprüft werden. Über `Restart` wird der Kernel neu gestartet und alle Variablen werden gelöscht.

Beim Ausführen einer Zelle wird Markdown in HTML-Preview übersetzt und der jeweilige Pythoncode ausgeführt:
![alt text](<.images/Pasted image 20261027113722.png>)

Hier ist eine generelle Übersicht über die wichtigsten Elemente eines Jupyter Notebooks:

![alt text](<.images/jupyter_toolbar_uebersicht.png>)
*Source: Claude*

Wichtig: Die Ausführungsnummer kann in die Irre führen. Wenn eine Zelle weiter oben [12] zeigt und eine darunter [5], wurde die obere zuletzt ausgeführt. Der Zustand des Notebooks hängt also von der Reihenfolge der Ausführung ab und nicht davon, wo die Zelle steht. Nach einem Kernel-Neustart beginnt die Zählung wieder bei 1.

>**Ziel 3: erfüllt**

---
# Part II
## Installation von WSL
*Dies betrifft nur Windows User*
> Da im weiteren Verlauf der Vorlesungsreihe Vibe Coding eingeführt wird, benötigen wir eine passende Infrastruktur dafür. Das IDM bietet dafür eigens entwickelte LLM an, die in [OpenCode](https://opencode.ai/de) (OpenSource Agent) verwendet werden können. OpenCode läuft nur auf Unix-basierten Betriebssystemen (Linux oder MacOS) und kann unter Windows nur in WSL (Windows Subsystem for Linux) betrieben werden.

Die [Installation](https://learn.microsoft.com/en-us/windows/wsl/setup/environment#get-started) ist einfach: es wird eine Powershell geöffnet und der Befehl `wsl --install` ausgeführt. Der Installationsanweisung ist zu folgen. Es wird nach einem `root` Passwort gefragt werden. Dieses solltet ihr euch sicher notieren, da dies das Superuser Passwort ist. Nach der Installation startet ihr WSL und legt euren lokaler Benutzer an. Die weiteren Schritte, welche in der Anleitung dokumentiert sind, müssen nicht ausgeführt werden.
## Installation von OpenCode
In der Ubuntu shell (WSL) wird `curl -fsSL https://opencode.ai/install | bash` ausgeführt. Mit `opencode --version` kann überprüft werden, ob die Installation erfolgreich war (Anzeige der installierten Version).
Im Anschluss wird Node.js installiert: `sudo apt install npm`

Um OpenCode mit den IDM-LLMs zu verwenden, müssen zwei Konfigurationsdateien sowie einige Umgebungsvariablen gesetzt werden.
### opencode.json
Zuerst wird der entsprechende Ordner angelegt, im Anschluss die Datei:
```
cd 
mkdir .config/opencode
cd .config/opencode
vi opencode.json
```

Nun öffnet sich eine neue Datei. Mit `i` wechselt man in den "insert" mode, es kann also editiert werden.
Der folgende Inhalt wird kopiert und mittels Rechtsklick in die neue Datei eingefügt:
```
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "llmchat-idm": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "llmchat-idm",
      "options": {
        "baseURL": "https://llm.idm.uk-augsburg.science/api"
      },
      "models": {
        "Qwen/Qwen3.8-Flash-Next-FP8": {
          "name": "Qwen/Qwen3.8-Flash-Next-FP8",
          "modalities": {
            "input": ["text", "image"],
            "output": ["text"]
          },
          "limit": {
            "context": 262144,
            "output": 86192
          }
        }
      }
    }
  },
  "permission": {
    "websearch": "allow"
  }
}
```
Im Anschluss den Editiermodus über `Esc` verlassen und die Datei mittels `:wq` + Enter schreiben und schließen (write and quit).
### auth.json
Hier wird ähnlich verfahren:
```
cd 
mkdir .local/share/opencode
cd .local/share/opencode
vi auth.json
```

Über `i` wieder in den Editiermodus wechseln und den unten stehenden Text reinkopieren:
```
{
  "llmchat-idm": {
    "type": "api",
    "key": "<PLACEHOLDER>"
  }
}
```

Der API Key für den LLM Chat wird zur Vibe Coding Vorlesung bekannt gegeben. Dieser ersetzt dann  `<PLACEHOLDER>`, die Anführungszeichen bleiben bestehen. Die Datei schließen (`Esc`, dann `:wq` + Enter).
### bashrc
Im Anschluss muss der OpenCode Pfad dem PATH hinzugefügt werden. Dazu wird die `.bashrc` Datei geöffnet: `vi ~/.bashrc`.
Folgender Text wird and Dateiende eingefügt (`i`):
```
# opencode
export PATH=${HOME}/.opencode/bin:$PATH
```

Schreiben und schließen (`Esc`, dann `:wq` + Enter). Um die Änderungen zu aktivieren, muss `source ~/.bashrc` ausgeführt werden. **Fertig**!

OpenCode kann nun in der Ubuntu Shell über opencode geöffnet werden.
