# Prozesssteckbrief: Elternbeiträge für Kinder in Kindertageseinrichtungen erheben

## Zusammenfassung
Der Prozess **"Elternbeiträge für Kinder in Kindertageseinrichtungen erheben"** beschreibt die Festsetzung und Einziehung der monatlichen Beiträge von Eltern, deren Kinder eine Kindertageseinrichtung besuchen. Der Prozess beginnt mit dem Bestehen eines Betreuungsverhältnisses, führt über die Anforderung und Prüfung von Einkommensnachweisen, die automatisierte Berechnung des Beitrags, bis hin zum Versand des Beitragsbescheids und der abschließenden Zahlung durch die Eltern. Ziel ist eine effiziente, transparente und rechtssichere Beitragsfestsetzung unter Einbindung der Eltern, des Jugendamtes und der IT-Systeme.

## Stammdaten
| Attribut | Wert |
| :--- | :--- |
| **Prozessname** | Elternbeiträge für Kinder in Kindertageseinrichtungen erheben |
| **Prozesskategorie** | Soziales & Familie |
| **Auslöser** | Betreuungsverhältnis besteht |
| **Ergebnis** | Elternbeitrag erhoben und Zahlung bestätigt |
| **Hauptverantwortung** | Jugendamt |
| **Beteiligte Rollen** | Bürger (Eltern), Jugendamt, IT |

## Prozessziele
1. **Effizienz:** Minimierung der Gesamtdurchlaufzeit von der Anforderung der Unterlagen bis zum Versand des Bescheids durch automatisierte Berechnungen und klare Prozessschritte.
2. **Qualität:** Sicherstellung einer hohen Daten- und Berechnungsqualität, um die Anzahl fehlerhafter Bescheide und nachfolgender Korrekturen zu minimieren.
3. **Rechtssicherheit:** Gewährleistung, dass die Beitragsfestsetzung konform mit den lokalen Satzungen und gesetzlichen Vorgaben erfolgt.
4. **Serviceorientierung:** Schaffung eines transparenten und nachvollziehbaren Verfahrens für die Eltern durch klare Kommunikation und definierte Fristen.

## Key Performance Indicators (KPIs)

Die folgenden Kennzahlen dienen der Messung der Prozessleistung und werden in Prozess-KPIs (Gesamtbetrachtung) und Aktivitäts-KPIs (Schrittbetrachtung) unterteilt.

### 1. Prozess-KPIs (Ebene Gesamtprozess)

Diese KPIs messen den Erfolg des gesamten End-to-End-Prozesses.

| KPI-ID | Kennzahl | Beschreibung | Zielwert | Messmethode |
| :--- | :--- | :--- | :--- | :--- |
| **P-KPI-01** | **Gesamtdurchlaufzeit** | Misst die Zeit vom Anfordern der Unterlagen bis zum Versand des Beitragsbescheids an die Eltern. | < 20 Arbeitstage | Timestamp(Task_Beitragsbescheid_versenden) - Timestamp(Task_Unterlagen_anfordern) |
| **P-KPI-02** | **Prozessqualität (First-Time-Right)** | Anteil der Beitragsbescheide, die ohne inhaltliche oder formale Korrekturen im ersten Anlauf korrekt sind. | > 98% | (Anzahl korrekter Bescheide / Gesamtanzahl Bescheide) * 100 |
| **P-KPI-03** | **Automatisierungsgrad der Berechnung** | Anteil der Elternbeiträge, die vollständig automatisiert durch das IT-System ohne manuelle Eingriffe berechnet werden. | > 95% | (Anzahl automatisch berechneter Fälle / Gesamtzahl der Fälle) * 100 |

### 2. Aktivitäts-KPIs (Ebene Prozessschritte)

Diese KPIs sind spezifischen Aktivitäten oder Phasen im BPMN-Modell zugeordnet, um Engpässe zu identifizieren.

| Zugeordnete Aktivität(en) | KPI-Name | Beschreibung & Relevanz | Zielwert |
| :--- | :--- | :--- | :--- |
| **Task_Unterlagen_anfordern** (Jugendamt) → **Event_Nachweise_eingegangen** (Jugendamt) | **Time-to-Submit** | Misst die Zeit, die Eltern benötigen, um ihre Einkommensnachweise nach der Anforderung einzureichen. Relevant zur Identifikation von Verzögerungen auf Bürgerseite. | < 14 Tage |
| **Event_Nachweise_eingegangen** (Jugendamt) → **Event_Berechnungsergebnis_erhalten** (Jugendamt) | **Time-to-Calculate** | Misst die Dauer der automatisierten Prüfung und Berechnung im IT-System. Ein hoher Wert deutet auf technische Engpässe hin. | < 1 Arbeitstag |
| **Task_IT_Einkommensdaten_pruefen** (IT) → **Task_IT_Elternbeitrag_berechnen** (IT) | **Daten-Validierungsrate** | Anteil der eingereichten Unterlagen, deren Daten vom IT-System ohne Fehler oder Plausibilitätswarnungen verarbeitet werden können. | > 90% |
| **Event_Berechnungsergebnis_erhalten** (Jugendamt) → **Task_Beitrag_festsetzen** (Jugendamt) | **Bearbeitungszeit Festsetzung** | Misst die Zeit, die die Sachbearbeitung benötigt, um das maschinelle Ergebnis zu prüfen und den Beitrag final festzusetzen. | < 2 Arbeitstage |
| **Task_Beitragsbescheid_versenden** (Jugendamt) → **Task_Elternbeitrag_entrichten** (Bürger) | **Zahlungsfrist-Einhaltung** | Anteil der Eltern, die den festgesetzten Beitrag innerhalb der im Bescheid genannten Frist entrichten. | > 95% |

## Eingesetzte IT-Systeme
- **Fachverfahren Kita-Beiträge:** Kernanwendung zur Verwaltung der Betreuungsverhältnisse, Berechnung der Elternbeiträge und Erstellung der Bescheide.
- **Dokumenten-Management-System (DMS):** Archivierung der eingereichten Einkommensnachweise und der versandten Beitragsbescheide.
- **Bürger-Service-Portal:** Digitale Plattform für Eltern zur Einreichung von Nachweisen und zur Kommunikation mit dem Jugendamt.

## Referenzdokumente
- BPMN-Modell: `Elternbeitraege_erheben.bpmn`
- Formular: `Elternbeitraege_Unterlagen_anfordern.form`
- Lokale Satzung über die Erhebung von Elternbeiträgen für Kindertageseinrichtungen
- SGB VIII (Kinder- und Jugendhilfegesetz)

---
