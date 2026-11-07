---
title: "LM Studio and Ollama for local AI"
description: "Short overview of LM Studio and Ollama for running small AI models locally with CPU only. Created with AI support."
categories: [AI]
tags: [Ollama,LM-Studio,Qwen,Llama,SmolLM,SmolVLM,Moondream,Whisper]
---

Sowohl **LM Studio** als auch **Ollama** sind beliebte Werkzeuge, um große Sprachmodelle (LLMs) komplett lokal auf dem eigenen Computer auszuführen – ohne Cloud und unter vollständiger Wahrung des Datenschutzes. Sie verfolgen jedoch völlig unterschiedliche Ansätze.


### Was ist LM Studio?

**LM Studio** ist eine **Desktop-Anwendung mit grafischer Benutzeroberfläche (GUI)**. Man kann sich das wie einen App-Store und Chat-Client für lokale KIs vorstellen.

* **Kernmerkmale:** Integrierter Modell-Browser (direkte Anbindung an Hugging Face), bequeme Regler für Parameter wie Temperatur und Kontextlänge, Dokumenten-Chat (RAG) und die Möglichkeit, einen OpenAI-kompatiblen lokalen API-Server per Klick zu starten.
* **Zielgruppe:** Nutzer, die eine visuelle, unkomplizierte Bedienung schätzen und direkt loslegen möchten, ohne im Terminal zu arbeiten.

### Was ist Ollama?

**Ollama** ist eine **leichtgewichtige Laufzeitumgebung (Engine / CLI-Tool)**, die primär im Hintergrund oder über das Terminal bedient wird.

* **Kernmerkmale:** Läuft minimalistisch als Hintergrunddienst (Daemon). Modelle werden über einfache Befehle (z. B. `ollama run llama3`) geladen und gesteuert. Ollama stellt standardmäßig eine lokale API zur Verfügung, die sich nahtlos in unzählige Entwickler-Tools, Skripte oder Frontends (wie Open WebUI) integrieren lässt.
* **Zielgruppe:** Entwickler, Server-Administratoren oder Nutzer, die KIs unauffällig im Hintergrund laufen lassen oder in eigene Anwendungen einbinden wollen.


### Die Hauptunterschiede im Überblick

| Kriterium | LM Studio | Ollama |
| --- | --- | --- |
| **Bedienung** | Grafische Benutzeroberfläche (GUI) | Kommandozeile / Terminal (CLI) |
| **Fokus** | Desktop-Nutzung, Chatten, visuelles Tuning & Experimentieren | Hintergrunddienst, Automatisierung, API-Integration für Apps |
| **Modell-Suche** | Komfortabler In-App-Store (Suche nach Hugging Face GGUF-Modellen) | Textbasierter Download via Befehl (`ollama pull`) |
| **Ressourcen** | Etwas höherer RAM-Verbrauch durch die Electron-Oberfläche | Extrem schlank und ressourcensparend |
| **Server-Betrieb** | Mittlerweile auch im Headless-Modus möglich, aber primär für Desktop konzipiert | Perfekt für Server und Docker-Container geeignet |


### Installation unter Windows und Linux

#### 1. LM Studio installieren

* **Unter Windows:**
1. Gehe auf die offizielle Website [lmstudio.ai](https://lmstudio.ai/).
2. Lade den Windows-Installer herunter.
3. Führe die `.exe`-Datei aus und folge den Anweisungen auf dem Bildschirm (Standard-Installation).
4. Starte LM Studio über die Desktop-Verknüpfung.


* **Unter Linux:**
1. LM Studio wird für Linux als **AppImage** angeboten.
2. Lade das AppImage von der offiziellen Website herunter.
3. Mache die Datei ausführbar (entweder per Rechtsklick $\rightarrow$ Eigenschaften $\rightarrow$ „Datei als Programm ausführen erlauben“ oder im Terminal: `chmod +x LM-Studio-*.AppImage`).
4. Doppelklicke auf die Datei oder starte sie im Terminal mit `./LM-Studio-*.AppImage`. *(Hinweis: Auf minimalen Linux-Systemen wird eventuell das Paket `libfuse2` benötigt).*



#### 2. Ollama installieren

* **Unter Windows:**
1. Gehe auf [ollama.com](https://ollama.com/) und lade den Windows-Installer herunter.
2. Führe die Installationsdatei aus. Ollama richtet sich automatisch als Windows-Dienst ein, der im Hintergrund läuft.
3. Öffne die **Windows PowerShell** oder die Eingabeaufforderung und teste die Installation mit:
```bash
ollama -v

```


4. Lade und starte dein erstes Modell direkt im Terminal, z. B.:
```bash
ollama run gemma:2b

```




* **Unter Linux:**
1. Ollama lässt sich am einfachsten über ein offizielles Installationsskript im Terminal einrichten. Führe dazu diesen Befehl aus:
```bash
curl -fsSL https://ollama.com/install.sh | sh

```


2. Das Skript installiert die Binärdateien und richtet Ollama als `systemd`-Dienst ein, der automatisch im Hintergrund startet.
3. Überprüfe die Installation:
```bash
ollama -v

```


4. Starte ein Modell via:
```bash
ollama run llama3

```


### Fazit: Welches solltest du wählen?

* Nimm **LM Studio**, wenn du direkt loschatten, verschiedene Modelle visuell durchstöbern und Einstellungen bequem per Mausklick regeln möchtest.
* Nimm **Ollama**, wenn du einen unauffälligen Hintergrunddienst suchst, Skripte schreibst oder lokale KIs an andere Software (wie Programmierumgebungen oder Web-Oberflächen) anbinden willst.

## Modelle

Für die Nutzung auf einem Notebook ohne dedizierte Grafikkarte (nur CPU) sind Sub-1B-Modelle (unter 1 Milliarde Parameter) ideal. Sie benötigen oft **unter 1 GB Arbeitsspeicher (RAM)**, reagieren extrem schnell und belasten den Akku kaum.

Um sie auf der CPU effizient auszuführen, nutze am besten quantisierte Versionen (z. B. **GGUF-Format** über Ollama oder LM Studio).



### 1. Reine Sprachmodelle (LLM)

Diese Modelle sind für Textgenerierung, Zusammenfassungen, Übersetzungen, RAG und einfache Programmieraufgaben auf der CPU optimiert:

* **Qwen2.5-0.5B** *(Alibaba)* – *Der aktuelle Preis-Leistungs-Sieger*
  ** **Größe:** ~0,5 Milliarden Parameter (benötigt ~400–600 MB RAM)
  ** **Stärken:** Überraschend stark in Deutsch, sehr gut im Verstehen von Befehlen (Instruction Following) und einfachem Coding. Für die Größe extrem leistungsfähig.


* **Llama-3.2-1B** *(Meta)* – *Der Standard für kleine Modelle*
  ** **Größe:** ~1,1 Milliarden Parameter (knapp über der 1B-Grenze, benötigt ~800 MB–1,2 GB RAM)
  ** **Stärken:** Hervorragendes Allgemeinwissen, sehr flüssige Texte, exzellente Unterstützung im Open-Source-Ökosystem.


* **SmolLM2-360M / SmolLM2-135M** *(Hugging Face)* – *Die Ultraschlanken*
  ** **Größe:** 135 Mio. bis 360 Mio. Parameter (benötigt nur ~200–400 MB RAM)
  ** **Stärken:** Extrem schnell auf jeder CPU. Perfekt für sehr einfache Textaufgaben, JSON-Formattierungen oder zum Testen von Pipelines.


* **Granite-3.0-1B-Instruct** *(IBM)* – *Für Business & Daten*
  ** **Größe:** ~1 Milliarde Parameter
  ** **Stärken:** Speziell auf Unternehmensaufgaben, Tabellen und Strukturierung ausgelegt.



---

### 2. Multimodale Modelle (LVM / LVA – Bild- & Audioverständnis)

Echte multimodale Vision- (LVM) oder Audio-Modelle (LVA) **unter 1B Parametern**, die lokal auf der CPU flüssig laufen, sind selten, da die Bild-/Audio-Encoder meist schon recht groß sind. Es gibt jedoch hervorragende kompakte Spezialmodelle:

#### Vision-Modelle (LVM – Bildverarbeitung)

* **Moondream2** *(Spezialisiertes Vision-Model)*
* **Größe:** ~1,8B Parameter (etwas über 1B, aber sehr leichtgewichtig)
* **Stärken:** Eines der schnellsten lokalen Vision-Modelle. Kann Bilder analysieren, Objekte beschreiben, Text auf Bildern lesen (OCR) und Fragen zu Bildern beantworten. Läuft auf modernen CPUs sehr passabel.


* **SmolVLM-256M / SmolVLM-500M** *(Hugging Face)*
* **Größe:** 256 Mio. bis 500 Mio. Parameter (echtes Sub-1B Vision-Modell)
* **Stärken:** Liest Dokumente, analysiert Diagramme und versteht Bilder bei minimalem RAM-Verbrauch.



#### Audio-Modelle (LVA – Spracherkennung & Audio)

Für Audio auf der CPU nutzt man am besten spezialisierte Modelle statt riesiger All-in-One-LLMs:

* **Whisper (tiny / base / small)** *(OpenAI)* – *Speech-to-Text*
* **Größe:** 39 Mio. (tiny) bis 244 Mio. (small) Parameter
* **Stärken:** Der Standard für Sprachverarbeitung auf der CPU. Transkribiert Audio (auch Deutsch) extrem präzise und schnell.


* **Kokoro-82M** – *Text-to-Speech (Sprachausgabe)*
* **Größe:** Nur 82 Millionen Parameter
* **Stärken:** Liefert erstaunlich natürliche Sprachausgabe direkt auf der CPU ohne spürbare Verzögerung.



---

### Schnellstart-Befehle für Ollama

Falls du **Ollama** installiert hast, kannst du die kleinsten Modelle direkt im Terminal auf deiner CPU starten:

```bash
# Sehr starkes 0,5B Sprachmodell
ollama run qwen2.5:0.5b

# Metas kompaktes 1B Modell
ollama run llama3.2:1b

# Leichtgewichtiges SmolLM2
ollama run smollm2:360m

# Moondream für Bildanalysen (Vision)
ollama run moondream

```