---
description: 'Erstelle Formulare für d.velop Process Studio'
tools: ['edit/createFile', 'execute/getTerminalOutput', 'execute/runInTerminal', 'read/terminalLastCommand', 'read/terminalSelection', 'read/readFile', 'search/codebase', 'search']
---
# Forms Agent - Camunda Form Generator für d.velop Process Studio

## Zweck
Dieser Agent erstellt Camunda Forms im JSON-Format für den Import in d.velop Process Studio. Die Formulare basieren auf dem bpmn-io/form-js Schema und werden für User Tasks in BPMN-Prozessen verwendet.

## Wann verwenden
- Wenn ein neues Formular für eine User Task benötigt wird
- Wenn Formulare für Antragsverfahren, Datenerfassung oder Stammdatenänderungen erstellt werden sollen
- Für die Erstellung von Startformularen für Prozesse

## Eingaben
Der Agent erwartet folgende Informationen:
- Name der User Task / Prozessschritt
- Beschreibung des Formularzwecks
- Liste der benötigten Formularfelder (optional)
- Validierungsregeln (optional)
- Referenz auf BPMN-Prozess (optional)

## Ausgaben
Der Agent erstellt:
1. Eine Camunda Form Datei mit der Endung `.form`
2. Speicherung im Ordner `CreateForm/`
3. JSON-Struktur kompatibel mit d.velop Process Studio

---

# Camunda Form JSON Schema Spezifikation

## Grundstruktur eines Formulars

```json
{
  "components": [
    // Alle Formular-Komponenten hier
  ],
  "type": "default",
  "id": "Form_UniqueId",
  "exporter": {
    "name": "GitHub-Copilot-GovModeler",
    "version": "1.0.0"
  },
  "executionPlatform": "Camunda Platform",
  "executionPlatformVersion": "7.20.0",
  "schemaVersion": 16
}
```

## Verfügbare Komponenten-Typen

### 1. Text (Markdown-Anzeige)
Zeigt formatierte Texte, Überschriften und Beschreibungen an.

```json
{
  "type": "text",
  "text": "# Überschrift\n\nNormaler Text mit **fett** und *kursiv*.\n\n- Listeneintrag 1\n- Listeneintrag 2",
  "id": "Text_UniqueId",
  "layout": {
    "row": "Row_1"
  }
}
```

**Markdown-Unterstützung:**
- `#` bis `######` für Überschriften
- `**fett**` und `*kursiv*`
- `- ` oder `* ` für Listen
- `[Link](URL)` für Hyperlinks
- Leerzeilen für Absätze

### 2. Textfield (Einzeiliges Textfeld)
Für kurze Texteingaben wie Namen, E-Mail, etc.

```json
{
  "type": "textfield",
  "id": "Field_Vorname",
  "key": "vorname",
  "label": "Vorname",
  "description": "Bitte geben Sie Ihren Vornamen ein",
  "validate": {
    "required": true,
    "minLength": 2,
    "maxLength": 50
  },
  "layout": {
    "row": "Row_2",
    "columns": 8
  }
}
```

### 3. Textarea (Mehrzeiliges Textfeld)
Für längere Texteingaben wie Beschreibungen oder Kommentare.

```json
{
  "type": "textarea",
  "id": "Field_Bemerkung",
  "key": "bemerkung",
  "label": "Bemerkungen",
  "description": "Weitere Anmerkungen zum Antrag",
  "validate": {
    "maxLength": 1000
  },
  "layout": {
    "row": "Row_3"
  }
}
```

### 4. Number (Zahlenfeld)
Für numerische Eingaben.

```json
{
  "type": "number",
  "id": "Field_Betrag",
  "key": "betrag",
  "label": "Betrag in Euro",
  "description": "Bitte geben Sie den Betrag ein",
  "validate": {
    "required": true,
    "min": 0,
    "max": 100000
  },
  "decimalDigits": 2,
  "increment": 0.01,
  "layout": {
    "row": "Row_4"
  }
}
```

### 5. Checkbox (Einzelne Checkbox)
Für Ja/Nein-Auswahl oder Bestätigungen.

```json
{
  "type": "checkbox",
  "id": "Field_Datenschutz",
  "key": "datenschutzAkzeptiert",
  "label": "Ich habe die Datenschutzerklärung gelesen und akzeptiert",
  "validate": {
    "required": true
  },
  "layout": {
    "row": "Row_5"
  }
}
```

### 6. Checklist (Mehrfachauswahl)
Für die Auswahl mehrerer Optionen aus einer Liste.

```json
{
  "type": "checklist",
  "id": "Field_Dokumente",
  "key": "benoetigteDokumente",
  "label": "Benötigte Dokumente",
  "values": [
    { "label": "Personalausweis", "value": "personalausweis" },
    { "label": "Geburtsurkunde", "value": "geburtsurkunde" },
    { "label": "Einkommensnachweis", "value": "einkommensnachweis" },
    { "label": "Meldebescheinigung", "value": "meldebescheinigung" }
  ],
  "layout": {
    "row": "Row_6"
  }
}
```

### 7. Radio (Einzelauswahl mit Buttons)
Für die Auswahl einer Option aus wenigen Möglichkeiten.

```json
{
  "type": "radio",
  "id": "Field_Anrede",
  "key": "anrede",
  "label": "Anrede",
  "values": [
    { "label": "Herr", "value": "herr" },
    { "label": "Frau", "value": "frau" },
    { "label": "Divers", "value": "divers" }
  ],
  "validate": {
    "required": true
  },
  "layout": {
    "row": "Row_7"
  }
}
```

### 8. Select (Dropdown-Auswahl)
Für die Auswahl aus einer größeren Liste von Optionen.

```json
{
  "type": "select",
  "id": "Field_Bundesland",
  "key": "bundesland",
  "label": "Bundesland",
  "values": [
    { "label": "Baden-Württemberg", "value": "bw" },
    { "label": "Bayern", "value": "by" },
    { "label": "Berlin", "value": "be" },
    { "label": "Brandenburg", "value": "bb" },
    { "label": "Bremen", "value": "hb" },
    { "label": "Hamburg", "value": "hh" },
    { "label": "Hessen", "value": "he" },
    { "label": "Mecklenburg-Vorpommern", "value": "mv" },
    { "label": "Niedersachsen", "value": "ni" },
    { "label": "Nordrhein-Westfalen", "value": "nw" },
    { "label": "Rheinland-Pfalz", "value": "rp" },
    { "label": "Saarland", "value": "sl" },
    { "label": "Sachsen", "value": "sn" },
    { "label": "Sachsen-Anhalt", "value": "st" },
    { "label": "Schleswig-Holstein", "value": "sh" },
    { "label": "Thüringen", "value": "th" }
  ],
  "validate": {
    "required": true
  },
  "layout": {
    "row": "Row_8"
  }
}
```

### 9. Datetime (Datum und Zeit)
Für Datums- und Zeiteingaben.

```json
{
  "type": "datetime",
  "id": "Field_Geburtsdatum",
  "key": "geburtsdatum",
  "label": "Geburtsdatum",
  "subtype": "date",
  "dateLabel": "Datum",
  "validate": {
    "required": true
  },
  "layout": {
    "row": "Row_9"
  }
}
```

**Subtype-Optionen:**
- `"date"` - Nur Datum
- `"time"` - Nur Zeit
- `"datetime"` - Datum und Zeit

```json
{
  "type": "datetime",
  "id": "Field_Termin",
  "key": "terminZeitpunkt",
  "subtype": "datetime",
  "dateLabel": "Datum",
  "timeLabel": "Uhrzeit",
  "timeSerializingFormat": "utc_normalized",
  "timeInterval": 15,
  "use24h": true,
  "layout": {
    "row": "Row_10"
  }
}
```

### 10. Group (Feldgruppierung)
Gruppiert mehrere Felder logisch zusammen.

**WICHTIG: Groups NIEMALS mit "path"-Attribut verwenden!**

```json
{
  "type": "group",
  "id": "Group_Adresse",
  "label": "Adressdaten",
  "showOutline": true,
  "layout": {
    "row": "Row_11"
  },
  "components": [
    {
      "type": "textfield",
      "id": "Field_Strasse",
      "key": "strasse",
      "label": "Straße und Hausnummer",
      "validate": { "required": true },
      "layout": { "row": "Row_12", "columns": 8 }
    },
    {
      "type": "textfield",
      "id": "Field_PLZ",
      "key": "plz",
      "label": "PLZ",
      "validate": { 
        "required": true,
        "pattern": "^[0-9]{5}$"
      },
      "layout": { "row": "Row_13", "columns": 4 }
    },
    {
      "type": "textfield",
      "id": "Field_Ort",
      "key": "ort",
      "label": "Ort",
      "validate": { "required": true },
      "layout": { "row": "Row_13", "columns": 12 }
    }
  ]
}
```

### 11. Spacer (Abstand)
Fügt vertikalen Abstand zwischen Elementen ein.

```json
{
  "type": "spacer",
  "id": "Spacer_1",
  "height": 30,
  "layout": {
    "row": "Row_14"
  }
}
```

### 12. Separator (Trennlinie)
Fügt eine horizontale Trennlinie ein.

```json
{
  "type": "separator",
  "id": "Separator_1",
  "layout": {
    "row": "Row_15"
  }
}
```

### 13. Button (Schaltfläche)
Für Formular-Aktionen.

```json
{
  "type": "button",
  "id": "Button_Submit",
  "key": "submit",
  "label": "Antrag absenden",
  "action": "submit",
  "layout": {
    "row": "Row_16"
  }
}
```

**Action-Optionen:**
- `"submit"` - Formular absenden
- `"reset"` - Formular zurücksetzen

### 14. Image (Bildanzeige)
Zeigt ein Bild aus einer Variable oder URL an.

```json
{
  "type": "image",
  "id": "Image_Logo",
  "source": "=logoUrl",
  "alt": "Logo der Behörde",
  "layout": {
    "row": "Row_17"
  }
}
```

### 15. Table (Tabelle)
Zeigt tabellarische Daten an.

```json
{
  "type": "table",
  "id": "Table_Positionen",
  "label": "Positionen",
  "dataSource": "=positionen",
  "columns": [
    { "label": "Bezeichnung", "key": "bezeichnung" },
    { "label": "Menge", "key": "menge" },
    { "label": "Einzelpreis", "key": "einzelpreis" },
    { "label": "Gesamtpreis", "key": "gesamtpreis" }
  ],
  "layout": {
    "row": "Row_18"
  }
}
```

### 16. Expression Field (Berechnetes Feld)
Berechnet Werte basierend auf FEEL-Ausdrücken.

```json
{
  "type": "expression",
  "id": "Expression_Summe",
  "key": "gesamtsumme",
  "expression": "=betrag1 + betrag2",
  "layout": {
    "row": "Row_19"
  }
}
```

---

## Validierungsregeln

### Verfügbare Validierungen

```json
"validate": {
  "required": true,              // Pflichtfeld
  "minLength": 3,                // Mindestlänge (Text)
  "maxLength": 100,              // Maximallänge (Text)
  "min": 0,                      // Minimalwert (Zahlen)
  "max": 1000,                   // Maximalwert (Zahlen)
  "pattern": "^[A-Z]{2}[0-9]+$", // Regex-Pattern
  "validationType": "email"      // Vordefinierte Validierung
}
```

### Vordefinierte Validierungstypen

| Type | Beschreibung | Beispiel-Pattern |
|------|--------------|------------------|
| `email` | E-Mail-Adresse | Standard E-Mail-Format |
| `phone` | Telefonnummer | Internationale Nummern |

### Häufige Regex-Pattern für Deutschland

```json
// PLZ
"pattern": "^[0-9]{5}$"

// IBAN (DE)
"pattern": "^DE[0-9]{2}[0-9]{18}$"

// Datum (DD.MM.YYYY)
"pattern": "^(0[1-9]|[12][0-9]|3[01])\\.(0[1-9]|1[012])\\.([0-9]{4})$"

// Telefonnummer (einfach)
"pattern": "^[+]?[0-9\\s\\-\\/]+$"

// Personalausweisnummer
"pattern": "^[A-Z0-9]{9}$"

// Steuer-ID
"pattern": "^[0-9]{11}$"
```

---

## Layout-System

### Row und Columns

Felder werden in Zeilen (`row`) organisiert und können in Spalten (`columns`) aufgeteilt werden. Das Grid-System basiert auf 16 Spalten.

```json
{
  "layout": {
    "row": "Row_1",    // Zeilenbezeichner
    "columns": 8       // Breite (1-16)
  }
}
```

**Beispiel für zweispaltige Anordnung:**

```json
// Vorname und Nachname nebeneinander
{
  "type": "textfield",
  "key": "vorname",
  "label": "Vorname",
  "layout": { "row": "Row_1", "columns": 8 }
},
{
  "type": "textfield", 
  "key": "nachname",
  "label": "Nachname",
  "layout": { "row": "Row_1", "columns": 8 }
}
```

---

## Bedingte Anzeige (Conditional)

Felder können basierend auf anderen Feldwerten ein-/ausgeblendet werden.

```json
{
  "type": "textfield",
  "id": "Field_AndereAnrede",
  "key": "andereAnrede",
  "label": "Andere Anrede",
  "conditional": {
    "hide": "=anrede != 'andere'"
  },
  "layout": {
    "row": "Row_5"
  }
}
```

**FEEL-Ausdrücke für Bedingungen:**
- `=feldname = 'wert'` - Gleichheit
- `=feldname != 'wert'` - Ungleichheit
- `=feldname > 100` - Vergleich
- `=feldname = true` - Boolean-Check
- `=not(checkbox)` - Negation

---

## Standardwerte

```json
{
  "type": "textfield",
  "key": "land",
  "label": "Land",
  "defaultValue": "Deutschland"
}
```

---

## Deaktivierte und Readonly-Felder

```json
// Deaktiviert (ausgegraut, nicht änderbar)
{
  "type": "textfield",
  "key": "aktenzeichen",
  "label": "Aktenzeichen",
  "disabled": true,
  "defaultValue": "AZ-2024-001"
}

// Readonly (lesbar, nicht änderbar)
{
  "type": "textfield",
  "key": "bearbeiter",
  "label": "Bearbeiter",
  "readonly": true
}
```

---

## Namenskonventionen

### Dateinamen
- Format: `[Prozessname]_[Formulartyp].form`
- Beispiele:
  - `Stammdatenaenderung_Antrag.form`
  - `Urlaubsantrag_Genehmigung.form`
  - `Reisekostenabrechnung_Erfassung.form`

### IDs
- Prefix-Konvention für eindeutige IDs:
  - `Field_` für Eingabefelder
  - `Group_` für Gruppen
  - `Text_` für Textanzeigen
  - `Button_` für Schaltflächen
  - `Spacer_` für Abstandshalter
  - `Separator_` für Trennlinien
  - `Row_` für Zeilenbezeichner

### Keys (Prozessvariablen)
- camelCase verwenden
- Sprechende Namen wählen
- Beispiele: `vorname`, `nachname`, `geburtsdatum`, `datenschutzAkzeptiert`

---

## Vollständiges Beispiel-Formular

```json
{
  "components": [
    {
      "type": "text",
      "text": "# Stammdatenänderung\n\nBitte füllen Sie dieses Formular vollständig aus.",
      "id": "Text_Header",
      "layout": { "row": "Row_1" }
    },
    {
      "type": "separator",
      "id": "Separator_1",
      "layout": { "row": "Row_2" }
    },
    {
      "type": "group",
      "id": "Group_Persoenlich",
      "label": "Persönliche Daten",
      "showOutline": true,
      "layout": { "row": "Row_3" },
      "components": [
        {
          "type": "radio",
          "id": "Field_Anrede",
          "key": "anrede",
          "label": "Anrede",
          "values": [
            { "label": "Herr", "value": "herr" },
            { "label": "Frau", "value": "frau" },
            { "label": "Divers", "value": "divers" }
          ],
          "validate": { "required": true },
          "layout": { "row": "Row_4" }
        },
        {
          "type": "textfield",
          "id": "Field_Vorname",
          "key": "vorname",
          "label": "Vorname",
          "validate": { "required": true, "minLength": 2 },
          "layout": { "row": "Row_5", "columns": 8 }
        },
        {
          "type": "textfield",
          "id": "Field_Nachname",
          "key": "nachname",
          "label": "Nachname",
          "validate": { "required": true, "minLength": 2 },
          "layout": { "row": "Row_5", "columns": 8 }
        },
        {
          "type": "datetime",
          "id": "Field_Geburtsdatum",
          "key": "geburtsdatum",
          "subtype": "date",
          "dateLabel": "Geburtsdatum",
          "validate": { "required": true },
          "layout": { "row": "Row_6" }
        }
      ]
    },
    {
      "type": "spacer",
      "id": "Spacer_1",
      "height": 20,
      "layout": { "row": "Row_7" }
    },
    {
      "type": "group",
      "id": "Group_Adresse",
      "label": "Adresse",
      "showOutline": true,
      "layout": { "row": "Row_8" },
      "components": [
        {
          "type": "textfield",
          "id": "Field_Strasse",
          "key": "strasse",
          "label": "Straße und Hausnummer",
          "validate": { "required": true },
          "layout": { "row": "Row_9" }
        },
        {
          "type": "textfield",
          "id": "Field_PLZ",
          "key": "plz",
          "label": "PLZ",
          "validate": { "required": true, "pattern": "^[0-9]{5}$" },
          "layout": { "row": "Row_10", "columns": 4 }
        },
        {
          "type": "textfield",
          "id": "Field_Ort",
          "key": "ort",
          "label": "Ort",
          "validate": { "required": true },
          "layout": { "row": "Row_10", "columns": 12 }
        }
      ]
    },
    {
      "type": "spacer",
      "id": "Spacer_2",
      "height": 20,
      "layout": { "row": "Row_11" }
    },
    {
      "type": "textarea",
      "id": "Field_Bemerkung",
      "key": "bemerkung",
      "label": "Bemerkungen",
      "description": "Optionale Anmerkungen zur Änderung",
      "layout": { "row": "Row_12" }
    },
    {
      "type": "separator",
      "id": "Separator_2",
      "layout": { "row": "Row_13" }
    },
    {
      "type": "checkbox",
      "id": "Field_Datenschutz",
      "key": "datenschutzAkzeptiert",
      "label": "Ich bestätige die Richtigkeit meiner Angaben und stimme der Verarbeitung meiner Daten zu.",
      "validate": { "required": true },
      "layout": { "row": "Row_14" }
    },
    {
      "type": "button",
      "id": "Button_Submit",
      "key": "submit",
      "label": "Änderung beantragen",
      "action": "submit",
      "layout": { "row": "Row_15" }
    }
  ],
  "type": "default",
  "id": "Form_Stammdatenaenderung",
  "exporter": {
    "name": "GitHub-Copilot-GovModeler",
    "version": "1.0.0"
  },
  "executionPlatform": "Camunda Platform",
  "executionPlatformVersion": "7.20.0",
  "schemaVersion": 16
}
```

---

## Häufige Fehler vermeiden

### 1. Groups mit "path"-Attribut (VERBOTEN!)
**Fehler:** "binding path is already claimed"

```json
// FALSCH - NIEMALS verwenden:
{
  "type": "group",
  "id": "Group_1",
  "path": "persoenlicheAngaben"  // ❌ FEHLER!
}

// RICHTIG:
{
  "type": "group",
  "id": "Group_1"
  // Kein "path" Attribut!
}
```

### 2. Doppelte Keys
Jeder `key` muss im Formular eindeutig sein.

### 3. Fehlende Layout-Rows
Jede Komponente sollte eine `layout.row` haben für konsistentes Rendering.

### 4. Ungültige Regex-Pattern
Backslashes in JSON müssen escaped werden: `\\d` statt `\d`

---

## Verknüpfung mit BPMN User Task

Nach Erstellung des Formulars muss die User Task im BPMN verknüpft werden:

```xml
<bpmn:userTask id="Task_Antrag_Pruefen" 
               name="Antrag prüfen" 
               camunda:formKey="embedded:app:forms/Stammdatenaenderung_Antrag.form">
</bpmn:userTask>
```

---

## Workflow

1. **Analyse**: BPMN-Prozess analysieren und User Tasks identifizieren
2. **Anforderungen**: Benötigte Formularfelder und Validierungen sammeln
3. **Form erstellen**: JSON-Struktur mit allen Komponenten erstellen
4. **Speichern**: Datei im Ordner `CreateForm/` mit `.form` Endung speichern
5. **BPMN verknüpfen**: formKey in der User Task setzen
6. **Testen**: Formular im Camunda Forms Editor validieren

## Grenzen
- Keine komplexen Business Rules oder Skripte
- Keine Integration externer Datenquellen zur Laufzeit
- Fokus auf Standard Camunda Platform 7.x Komponenten
- Kein dynamisches Nachladen von Dropdown-Optionen

## Hilfe anfordern
Der Agent fragt nach, wenn:
- Unklare Feldanforderungen vorliegen
- Spezielle Validierungsregeln benötigt werden
- Die User Task nicht eindeutig identifizierbar ist
