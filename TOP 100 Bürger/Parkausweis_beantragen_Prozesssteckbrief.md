# Prozesssteckbrief: Parkausweis beantragen

## Zusammenfassung
Der Prozess **"Parkausweis beantragen"** dient der digitalen Entgegennahme, Pruefung und Entscheidung ueber einen Antrag auf Erteilung eines Parkausweises. Der Prozess beginnt mit der Antragstellung durch den Buerger, fuehrt ueber eine automatisierte Datenpruefung durch ein IT-System sowie eine fachliche Pruefung durch die zustaendige Behoerde und endet mit der Zustellung des Bescheids. Ziel ist eine effiziente, transparente und rechtssichere Bearbeitung unter Einbindung aller beteiligten Stellen.

## Stammdaten
| Attribut | Wert |
| :--- | :--- |
| **Prozessname** | Parkausweis beantragen |
| **Prozesskategorie** | Buergerservice |
| **Auslöser** | Antrag auf Parkausweis eingegangen |
| **Ergebnis** | Parkausweis bewilligt und Bescheid zugestellt |
| **Hauptverantwortung** | Zustaendige Behoerde (z.B. Strassenverkehrsamt) |
| **Beteiligte Rollen** | Buerger, IT, Behoerde |

## Prozessziele
1. **Effizienz:** Die Gesamt-Durchlaufzeit von der Antragstellung bis zur Bescheidzustellung soll durch digitale Einreichung und automatisierte Vorpruefung minimiert werden.
2. **Qualitaet:** Eine hohe Datenqualitaet und vollstaendige Antraege sollen durch Pflichtfelder im Online-Formular und automatisierte Pruefungen sichergestellt werden, um Nachforderungen zu reduzieren.
3. **Serviceorientierung:** Buerger sollen den Antrag vollstaendig digital und medienbruchfrei einreichen koennen, was den Aufwand reduziert und den Service verbessert.
4. **Transparenz:** Der Prozess soll eine nachvollziehbare und transparente Entscheidungsgrundlage schaffen, indem alle Pruefschritte und Ergebnisse dokumentiert werden.

## Key Performance Indicators (KPIs)

Die folgenden Kennzahlen dienen der Messung der Prozessleistung und werden in Prozess-KPIs (Gesamtbetrachtung) und Aktivitäts-KPIs (Schrittbetrachtung) unterteilt.

### 1. Prozess-KPIs (Ebene Gesamtprozess)

Diese KPIs messen den Erfolg des gesamten End-to-End-Prozesses.

| KPI-ID | Kennzahl | Beschreibung | Zielwert | Messmethode |
| :--- | :--- | :--- | :--- | :--- |
| **P-KPI-01** | **Gesamt-Durchlaufzeit** | Zeit vom Eingang des Antrags (`StartEvent_Antrag_eingegangen`) bis zur Zustellung des Bescheids (`Event_Bescheid_erhalten`). | < 10 Arbeitstage | Timestamp(Event_Bescheid_erhalten) - Timestamp(StartEvent_Antrag_eingegangen) |
| **P-KPI-02** | **Erst-Antrags-Erfolgsquote** | Anteil der Antraege, die ohne manuelle Nachforderung von Unterlagen oder Korrekturen direkt bearbeitet werden koennen. | > 90% | (Anzahl Antraege ohne Nachforderung / Gesamtanzahl Antraege) * 100 |
| **P-KPI-03** | **Automatisierungsgrad der Vorpruefung** | Anteil der Antraege, bei denen die IT-Pruefung (Wohnsitz, Berechtigung) vollstaendig automatisiert ohne manuelle Intervention erfolgt. | > 95% | (Anzahl automatisch gepruefter Antraege / Gesamtanzahl Antraege) * 100 |

### 2. Aktivitäts-KPIs (Ebene Prozessschritte)

Diese KPIs sind spezifischen Aktivitäten oder Phasen im BPMN-Modell zugeordnet, um Engpaesse zu identifizieren.

| Zugeordnete Aktivität(en) | KPI-Name | Beschreibung & Relevanz | Zielwert |
| :--- | :--- | :--- | :--- |
| **Antrag absenden** (Buerger) → **Antrag pruefen** (Behoerde) | **Time-to-Acknowledge** | Zeit zwischen dem Absenden des Antrags durch den Buerger und dem Beginn der fachlichen Pruefung durch die Behoerde. Misst die Effizienz der Antragsannahme. | < 8 Stunden | Timestamp(Task_Antrag_pruefen) - Timestamp(Task_Antrag_absenden) |
| **Datenanfrage stellen** (Behoerde) → **Pruefergebnis erhalten** (Behoerde) | **IT-Antwortzeit** | Zeit, die das IT-System fuer die automatisierte Pruefung der Antragsdaten benoetigt. Ein zentraler Faktor fuer die Gesamtdauer. | < 5 Minuten | Timestamp(Event_Pruefergebnis_erhalten) - Timestamp(Task_Datenanfrage_stellen) |
| **Antrag registrieren** (IT) → **Pruefergebnis bereitstellen** (IT) | **IT-Verarbeitungszeit** | Reine Bearbeitungszeit innerhalb des IT-Systems (ohne Wartezeiten). Misst die technische Performance. | < 1 Minute | Timestamp(Task_Pruefergebnis_bereitstellen) - Timestamp(Task_Antrag_registrieren) |
| **Pruefergebnis erhalten** (Behoerde) → **Entscheidung treffen** (Behoerde) | **Fachliche Entscheidungszeit** | Zeit, die der Sachbearbeiter fuer die finale Bewertung und Entscheidung nach Erhalt aller Daten benoetigt. | < 3 Arbeitstage | Timestamp(Task_Entscheidung_treffen) - Timestamp(Event_Pruefergebnis_erhalten) |
| **Entscheidung treffen** (Behoerde) → **Bescheid versenden** (Behoerde) | **Bescheiderstellungszeit** | Zeit fuer die administrative Erstellung und den Versand des Bescheids nach getroffener Entscheidung. | < 1 Arbeitstag | Timestamp(Task_Bescheid_versenden) - Timestamp(Task_Entscheidung_treffen) |

## Eingesetzte IT-Systeme
- **Online-Antragsportal:** Stellt das digitale Formular `Parkausweis_Antrag.form` bereit und nimmt die Antragsdaten sowie Nachweise vom Buerger entgegen.
- **Backend-System (Fachverfahren):** Verarbeitet die Antragsdaten, fuehrt die automatisierten Pruefungen durch (z.B. Abgleich mit Melderegister) und stellt die Ergebnisse der Behoerde bereit.
- **Dokumentenmanagementsystem (DMS):** Archiviert den Antrag, die Nachweise und den Bescheid rechtssicher.

## Referenzdokumente
- BPMN-Modell: `CreateBPMN/Parkausweis_beantragen.bpmn`
- Antragsformular: `CreateForm/Parkausweis_Antrag.form`
- [Optional: Verweise auf lokale Strassenverkehrsordnung, Gebuehrenordnung]

---
