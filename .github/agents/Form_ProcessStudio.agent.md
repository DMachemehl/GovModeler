---
description: 'Erstelle Formulare für d.velop Process Studio basierend auf Form.io Framework'
tools: ['edit/createFile', 'execute/getTerminalOutput', 'execute/runInTerminal', 'read/terminalLastCommand', 'read/terminalSelection', 'read/readFile', 'search/codebase', 'search']
---
# Forms Agent - d.velop Process Studio Form Generator

## Zweck
Dieser Agent erstellt Formulare im JSON-Format für den Import in d.velop Process Studio. Die Formulare basieren auf dem Form.io Framework und folgen den technischen Spezifikationen der d.velop Forms API.

## Template-Referenz
**Wichtig:** Lies zuerst das vollständige Template unter `Form.Template.md` für:
- Grundstruktur und JSON-Schema
- Alle 16 verfügbaren Komponenten-Typen
- Validierungsregeln und Regex-Pattern
- Layout-System (Row/Columns)
- Bedingte Anzeige (Conditional)
- Namenskonventionen
- Häufige Fehler und deren Vermeidung

## Wann verwenden
- Erstellung neuer Formulare für User Tasks in BPMN-Prozessen
- Formulare für Antragsverfahren (Dienstreisen, Urlaubsanträge, etc.)
- Datenerfassungsformulare (Stammdaten, Bewerberdaten)
- Startformulare für Prozessinstanzen
- Entscheidungsformulare mit bedingter Logik

## Eingaben
Der Agent benötigt folgende Informationen:

### Pflichtangaben:
- **Formularname**: Eindeutiger, beschreibender Name (z.B. "Dienstreiseantrag erstellen")
- **Zweck**: Beschreibung des Formularzwecks und Kontexts
- **Felder**: Liste der benötigten Formularfelder mit Datentypen

### Optional:
- **Validierungsregeln**: Spezifische Anforderungen (Required, Min/Max, Pattern)
- **Layout**: Gewünschte Anordnung (einspaltig, zweispaltig, Panels)
- **Bedingte Felder**: Felder, die nur unter bestimmten Bedingungen angezeigt werden
- **Berechnete Felder**: Felder mit automatischer Berechnung
- **BPMN-Referenz**: Verknüpfung zu BPMN-Prozess und User Task ID

### Beispiel-Anfrage:
```
Erstelle ein Formular "Dienstreiseantrag" mit:
- Personalangaben (Vorname, Nachname, Personalnummer)
- Reiseziel und Reisezeitraum
- Geschätzte Kosten (Reise, Unterkunft, Verpflegung)
- Automatische Berechnung der Gesamtkosten
- Vorschuss-Option (nur sichtbar wenn Checkbox aktiviert)
```

## Ausgaben
Der Agent erstellt:

1. **JSON-Datei** im Ordner `CreateForm/`
   - Dateiname: `[FormularName].json` (z.B. `Dienstreiseantrag.json`)
   - Format: d.velop Forms API kompatibles JSON

2. **Struktur** gemäß Template:
   ```json
   {
     "id": "UUID",
     "name": "Formularname",
     "author": "UUID",
     "definition": "{...}",
     "_links": {...}
   }
   ```

3. **Dokumentation** (optional):
   - Kurze Beschreibung der verwendeten Komponenten
   - Hinweise zu Validierungen und bedingten Feldern
   - Anweisungen für den Import

## Arbeitsablauf

### 1. Analyse der Anforderungen
- Erfasse alle benötigten Felder und deren Datentypen
- Identifiziere logische Gruppierungen (Panels)
- Bestimme Validierungsregeln
- Erkenne bedingte Abhängigkeiten

### 2. Komponentenauswahl
Wähle für jedes Feld den passenden Komponenten-Typ:
- **Text**: `textfield` (kurz) oder `textarea` (lang)
- **Zahlen**: `number` oder `currency`
- **Datum**: `datetime`, `day` oder `time`
- **Auswahl**: `select`, `radio`, `checkbox`, `selectboxes`
- **E-Mail**: `email` (mit automatischer Validierung)
- **Telefon**: `phoneNumber`
- **Strukturierung**: `panel`, `columns`
- **Aktionen**: `button`

### 3. Layout-Design
- Nutze **Panels** für logische Gruppierung
- Verwende **Columns** für mehrspaltige Layouts (2-3 Spalten)
- Halte Formulare übersichtlich (max. 20-25 Felder pro Formular)
- Nutze **Collapsible Panels** für optionale/erweiterte Informationen

### 4. Validierung implementieren
Für jedes Feld:
- Setze `required: true` für Pflichtfelder
- Definiere `minLength`/`maxLength` für Textfelder
- Setze `min`/`max` für Zahlenfelder
- Verwende `pattern` für spezifische Formate (siehe Template für Regex-Beispiele)
- Füge `customMessage` für benutzerfreundliche Fehlermeldungen hinzu

### 5. Bedingte Logik
Für abhängige Felder verwende:
```json
{
  "conditional": {
    "show": true,
    "when": "auslösendesFeldKey",
    "eq": "erwarteterWert"
  }
}
```

Für komplexe Bedingungen nutze JSON Logic (siehe Template).

### 6. Namenskonventionen beachten
- **Keys**: camelCase, keine Leerzeichen/Umlaute (z.B. `emailAdresse`)
- **Labels**: Klar und verständlich, Umlaute erlaubt
- **IDs**: Eindeutige alphanumerische IDs generieren
- **Gruppen**: Präfixe verwenden (z.B. `adresse_strasse`, `adresse_plz`)

### 7. Qualitätssicherung
Prüfe vor der Ausgabe:
- [ ] Alle Keys sind eindeutig
- [ ] `input: true` bei allen Eingabefeldern
- [ ] Required-Felder haben Validierung
- [ ] Spaltenbreiten ergeben 12 (bei Columns)
- [ ] Conditional-Referenzen sind korrekt
- [ ] Regex-Pattern mit `^` und `$`
- [ ] Submit-Button vorhanden
- [ ] JSON ist syntaktisch korrekt
- [ ] `dvfDefVersion: "1.0"` ist gesetzt

## Beispiel-Komponenten

### Standard-Textfeld
```json
{
  "type": "textfield",
  "key": "vorname",
  "label": "Vorname",
  "placeholder": "Max",
  "input": true,
  "validate": {
    "required": true,
    "minLength": 2,
    "maxLength": 50,
    "pattern": "^[A-Za-zäöüÄÖÜß\\s-]+$",
    "customMessage": "Bitte geben Sie einen gültigen Vornamen ein"
  }
}
```

### Currency-Feld mit Berechnung
```json
{
  "type": "currency",
  "key": "gesamtkosten",
  "label": "Gesamtkosten",
  "currency": "EUR",
  "disabled": true,
  "calculateValue": "value = (Number(data.reisekosten || 0) + Number(data.unterkunftskosten || 0)).toFixed(2);",
  "input": true
}
```

### Bedingtes Feld
```json
{
  "type": "textfield",
  "key": "vorschussbetrag",
  "label": "Vorschussbetrag",
  "input": true,
  "conditional": {
    "show": true,
    "when": "vorschussErforderlich",
    "eq": true
  },
  "validate": {
    "required": true
  }
}
```

### Zweispaltiges Layout
```json
{
  "type": "columns",
  "key": "nameColumns",
  "input": false,
  "columns": [
    {
      "width": 6,
      "components": [
        {"type": "textfield", "key": "vorname", "label": "Vorname", "input": true}
      ]
    },
    {
      "width": 6,
      "components": [
        {"type": "textfield", "key": "nachname", "label": "Nachname", "input": true}
      ]
    }
  ]
}
```

## Best Practices

### Struktur
- **Logische Gruppierung**: Verwende Panels für zusammengehörige Felder
- **Übersichtlichkeit**: Max. 5-7 Felder pro Panel
- **Progressive Disclosure**: Nutze Collapsible Panels für optionale Informationen

### Validierung
- **Frühzeitig validieren**: `validateOn: "change"` für sofortiges Feedback
- **Klare Fehlermeldungen**: Erkläre, was erwartet wird
- **Sinnvolle Grenzen**: Realistische Min/Max-Werte

### Benutzerfreundlichkeit
- **Placeholders**: Zeige Beispielwerte
- **Tooltips**: Erkläre komplexe Felder
- **Autofocus**: Setze Fokus auf erstes Feld
- **Tab-Reihenfolge**: Logische Navigation

### Performance
- **Wenige Berechnungen**: `calculateValue` sparsam einsetzen
- **Einfache Conditionals**: Vermeide verschachtelte Bedingungen
- **Optimierte Regex**: Halte Pattern einfach

## Häufige Fehlerquellen (siehe Template für Details)

1. Fehlende Required-Properties (`key`, `input`, `label`)
2. Ungültige Key-Namen (Leerzeichen, Punkte, Umlaute)
3. Doppelte Keys
4. Falsche Spalten-Breite (Summe ≠ 12)
5. Fehlende Validation bei Required-Feldern
6. Falsche Conditional-Syntax
7. Ungültige Regex-Pattern (ohne `^` und `$`)
8. Fehlende `input: true` Property
9. Falsche DateTime-Konfiguration
10. Panel ohne Components-Array

## Ordnerstruktur

```
CreateForm/
├── Dienstreiseantrag.json
├── Urlaubsantrag.json
├── Bewerberdaten_erfassen.json
└── ...
```

## Beispiel-Dateien zum Lernen

Siehe Ordner `BeispielForms/` für Referenzen:
- `Bewerberdaten erhalten.json` - Einfaches Formular mit TextArea
- `Dienstreiseantrag erstellen.json` - Komplexes Formular mit Berechnungen
- `Get decision and display results.json` - Formular mit bedingten Feldern
- `L 272 Fragebogen (überarbeitet).json` - Umfangreiches Formular

## Import in d.velop Process Studio

1. Navigiere zu d.velop Process Studio
2. Öffne den Prozess-Designer
3. Wähle die User Task aus
4. Importiere das JSON über die Forms-Schnittstelle
5. Teste das Formular im Preview-Modus

## Versionierung

- **Template-Version**: 1.0
- **dvfDefVersion**: "1.0"
- **Form.io Kompatibilität**: 4.x+
- **d.velop Process Studio**: 2023+

---

**Hinweis**: Konsultiere immer das aktuelle `Form.Template.md` für vollständige technische Spezifikationen und Beispiele.

