# Technische Dokumentation - GovModeler

## Übersicht
Diese Dokumentation beschreibt die technischen Grundlagen und Voraussetzungen zur Nutzung des GovModelers für die KI-gestützte Erstellung von BPMN-Prozessmodellen.

## Systemvoraussetzungen

### Software-Anforderungen
- **Visual Studio Code** (Version 1.80 oder höher)
- **Git** (für Repository-Verwaltung)
- **GitHub Copilot Subscription** (Business, Enterprise oder Individual)

### Betriebssystem
- Windows 10/11
- macOS 10.15 oder höher
- Linux (Ubuntu 20.04 oder höher empfohlen)

## Erforderliche VS Code Extensions

### 1. GitHub Copilot (erforderlich)
**Extension ID:** `GitHub.copilot`

**Zweck:** KI-gestützte Code- und BPMN-Generierung

**Installation:**
```
ext install GitHub.copilot
```

**Empfohlene Einstellungen:**
```json
{
  "github.copilot.enable": {
    "*": true,
    "xml": true,
    "bpmn": true
  },
  "github.copilot.advanced": {
    "debug.overrideEngine": "gpt-4",
    "inlineSuggestEnable": true
  }
}
```

### 2. GitHub Copilot Chat (erforderlich)
**Extension ID:** `GitHub.copilot-chat`

**Zweck:** Interaktive Kommunikation mit Copilot für Prozessmodellierung

**Installation:**
```
ext install GitHub.copilot-chat
```

**Empfohlene Einstellungen:**
```json
{
  "github.copilot.chat.enabled": true,
  "github.copilot.chat.localeOverride": "de"
}
```

### 3. BPMN Editor (empfohlen)
**Extension ID:** `bpmn-io.vs-code-bpmn-io`

**Zweck:** Visuelle Darstellung und Bearbeitung von BPMN-Diagrammen

**Installation:**
```
ext install bpmn-io.vs-code-bpmn-io
```

**Konfiguration:**
```json
{
  "bpmn.modeling.enableXmlFormatting": true,
  "bpmn.modeling.autoSave": true
}
```

### 4. XML Tools (empfohlen)
**Extension ID:** `DotJoshJohnson.xml`

**Zweck:** XML-Syntax-Highlighting und Formatierung für BPMN-Dateien

**Installation:**
```
ext install DotJoshJohnson.xml
```

**Konfiguration:**
```json
{
  "xmlTools.enableXmlTreeView": true,
  "xmlTools.enforcePrettySelfClosingTagOnFormat": true,
  "xmlTools.splitXmlnsOnFormat": true
}
```

### 5. Markdown All in One (optional)
**Extension ID:** `yzhang.markdown-all-in-one`

**Zweck:** Bearbeitung der Dokumentationsdateien

**Installation:**
```
ext install yzhang.markdown-all-in-one
```

## VS Code Workspace-Konfiguration

### settings.json
Empfohlene Workspace-Einstellungen für optimale Nutzung:

```json
{
  "files.associations": {
    "*.bpmn": "xml"
  },
  "files.encoding": "utf8",
  "files.autoSave": "afterDelay",
  "files.autoSaveDelay": 1000,
  
  "editor.formatOnSave": true,
  "editor.formatOnPaste": true,
  "editor.wordWrap": "on",
  
  "[xml]": {
    "editor.defaultFormatter": "DotJoshJohnson.xml",
    "editor.formatOnSave": true
  },
  
  "[markdown]": {
    "editor.defaultFormatter": "yzhang.markdown-all-in-one",
    "editor.wordWrap": "on"
  },
  
  "search.exclude": {
    "**/node_modules": true,
    "**/.git": true
  }
}
```

### extensions.json
Für Team-Projekte empfohlene Extensions-Datei (`.vscode/extensions.json`):

```json
{
  "recommendations": [
    "github.copilot",
    "github.copilot-chat",
    "bpmn-io.vs-code-bpmn-io",
    "dotjoshjohnson.xml",
    "yzhang.markdown-all-in-one"
  ]
}
```

## Einrichtung und Workflow

### Schritt 1: Repository klonen
```bash
git clone https://github.com/ovaltinetippins/GovModeler_KOI.git
cd GovModeler_KOI
```

### Schritt 2: VS Code öffnen
```bash
code .
```

### Schritt 3: Extensions installieren
1. Öffnen Sie die Extensions-Ansicht (`Ctrl+Shift+X` / `Cmd+Shift+X`)
2. Installieren Sie die empfohlenen Extensions
3. Melden Sie sich bei GitHub Copilot an

### Schritt 4: BPMN-Template verwenden
Die Datei `BPMN_Template.xml` dient als Vorlage für neue Prozessmodelle.

## Nutzung mit GitHub Copilot

### BPMN-Generierung mit Copilot Chat
1. Öffnen Sie Copilot Chat (`Ctrl+Alt+I` / `Cmd+Alt+I`)
2. Verwenden Sie strukturierte Prompts wie:
   ```
   Erstelle ein BPMN 2.0 Prozessmodell für den Prozess 
   "Personalausweis beantragen" mit folgenden Schritten:
   - Antrag online ausfüllen
   - Dokumente hochladen
   - Termin vereinbaren
   - Persönlich erscheinen
   - Ausweis abholen
   ```

### Best Practices für Prompts
- Verwenden Sie die Guideline-Datei `BPMN-DI_Guidelines.md` als Referenz
- Geben Sie klare Prozessschritte vor
- Definieren Sie Rollen/Lanes explizit
- Nennen Sie Entscheidungspunkte (Gateways)

## Dateistruktur

```
GovModeler_KOI/
├── BPMN_Template.xml           # BPMN-Vorlage
├── BPMN-DI_Guidelines.md       # Richtlinien für BPMN-DI
├── README.md                    # Projekt-Übersicht
├── TECHNISCHE_DOKUMENTATION.md # Diese Datei
├── CreateBPMN/                 # Generierte BPMN-Modelle
└── TOP 100 Bürger/            # Spezielle Verwaltungsprozesse
```

## Versionierung und Collaboration

### Git-Workflow
```bash
# Neuen Branch für Prozessmodell erstellen
git checkout -b feature/neuer-prozess

# BPMN-Datei generieren und committen
git add CreateBPMN/neuer-prozess.bpmn
git commit -m "feat: Prozessmodell für [Prozessname] erstellt"

# Push und Pull Request
git push origin feature/neuer-prozess
```

### Commit-Konventionen
- `feat:` Neues Prozessmodell
- `fix:` Korrektur in bestehendem Modell
- `docs:` Dokumentationsänderungen
- `refactor:` Überarbeitung ohne funktionale Änderung

## Troubleshooting

### Problem: Copilot generiert kein BPMN
**Lösung:** 
- Prüfen Sie die Copilot-Subscription
- Stellen Sie sicher, dass XML-Dateien nicht in `.gitignore` ausgeschlossen sind
- Verwenden Sie explizite BPMN 2.0 Referenzen im Prompt

### Problem: BPMN-Visualisierung funktioniert nicht
**Lösung:**
- Installieren Sie die Extension `bpmn-io.vs-code-bpmn-io`
- Prüfen Sie ob die `.bpmn`-Datei valides XML ist
- Validieren Sie gegen BPMN 2.0 Schema

### Problem: XML-Formatierung fehlerhaft
**Lösung:**
- Installieren Sie XML Tools Extension
- Verwenden Sie `Format Document` (`Shift+Alt+F` / `Shift+Option+F`)

## Weiterführende Ressourcen

- [BPMN 2.0 Spezifikation](https://www.omg.org/spec/BPMN/2.0/)
- [GitHub Copilot Dokumentation](https://docs.github.com/copilot)
- [bpmn.io Dokumentation](https://bpmn.io/toolkit/bpmn-js/)

## Support und Kontakt

Bei Fragen oder Problemen:
- GitHub Issues: https://github.com/ovaltinetippins/GovModeler_KOI/issues
- Projektverantwortliche kontaktieren

---

**Stand:** Oktober 2025  
**Version:** 1.0
