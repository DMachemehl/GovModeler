# Prozesssteckbrief: Strategische Personalbedarfsplanung durchführen

## Zusammenfassung
Der Prozess **"Strategische Personalbedarfsplanung durchführen"** erfasst systematisch den mittel- bis langfristigen Personalbedarf der Organisation auf Basis prognostizierter Veränderungen (Rentenabgänge, Organisationsentwicklung, Bedarfsentwicklung). Er beginnt mit der Meldung eines Planungsbedarfs, führt über eine IT-gestützte Datenerfassung, Konsolidierung und Berechnung zur Erstellung von Bedarfsprognosen und endet mit der verbindlichen Freigabe und Veröffentlichung eines strategischen Planungsberichts. Ziel ist die vorausschauende Steuerung der Personalressourcen zur Sicherstellung der Handlungsfähigkeit der Organisation.

## Stammdaten
| Attribut | Wert |
| :--- | :--- |
| **Prozessname** | Strategische Personalbedarfsplanung durchführen |
| **Prozesskategorie** | Personalstrategie |
| **Auslöser** | Planungsbedarf entstanden (strategischer Planungslauf angestoßen) |
| **Ergebnis** | Strategische Personalbedarfsplanung abgeschlossen (Planungsbericht liegt vor) |
| **Hauptverantwortung** | Personalstelle zentral |
| **Beteiligte Rollen** | Bedarfsträger (Fachbereiche/Führungskräfte), IT (Planungssystem), Personalstelle zentral |

## Prozessziele
1. **Strategische Steuerung:** Ermöglichung einer datenbasierten, zukunftsorientierten Personalstrategie zur rechtzeitigen Deckung von Bedarfslücken (z. B. durch Rentenabgänge).
2. **Planungssicherheit:** Schaffung verlässlicher Grundlagen für Stellenbesetzungen, Ausbildungsplanung und Budgetentscheidungen.
3. **Transparenz & Datenqualität:** Sicherstellung valider, nachvollziehbarer und konsistenter Planungsdaten durch automatisierte IT-Unterstützung.
4. **Frühwarnsystem:** Rechtzeitige Identifikation kritischer Personalengpässe zur Vermeidung von Versorgungslücken oder Know-how-Verlust.
5. **Effizienz:** Automatisierung der Datenerfassung und Berechnung zur Entlastung der Fachbereiche und Personalstellen.

## Key Performance Indicators (KPIs)

Die folgenden Kennzahlen dienen der Messung der Prozessleistung und werden in Prozess-KPIs (Gesamtbetrachtung) und Aktivitäts-KPIs (Schrittbetrachtung) unterteilt.

### 1. Prozess-KPIs (Ebene Gesamtprozess)

Diese KPIs messen den Erfolg des gesamten End-to-End-Prozesses.

| KPI-ID | Kennzahl | Beschreibung | Zielwert | Messmethode |
| :--- | :--- | :--- | :--- | :--- |
| **P-KPI-01** | **Planungszyklus-Durchlaufzeit** | Gesamtdauer von der Bedarfsmeldung bis zur finalen Veröffentlichung des Planungsberichts | < 6 Wochen (regulärer Zyklus) | Enddatum(Veröffentlichung) - Startdatum(Bedarfsmeldung) |
| **P-KPI-02** | **Prognosegenauigkeit** | Übereinstimmung der prognostizierten mit den tatsächlich eingetretenen Personalabgängen nach 12 Monaten | > 85% Trefferquote | Vergleich Prognose vs. Ist-Abgänge |
| **P-KPI-03** | **Datenaktualität** | Anteil der Planungsdaten, die nicht älter als 3 Monate sind | > 95% | Zeitstempel-Analyse der Eingangsdaten |
| **P-KPI-04** | **Abdeckungsgrad** | Anteil der organisatorischen Einheiten, die in die strategische Planung einbezogen wurden | 100% | Anzahl erfasster OE / Gesamt-OE |

### 2. Aktivitäts-KPIs (Ebene Prozessschritte)

Diese KPIs sind spezifischen Aktivitäten oder Phasen im BPMN-Modell zugeordnet, um Engpässe zu identifizieren.

| Zugeordnete Aktivität(en) | KPI-Name | Beschreibung & Relevanz | Zielwert |
| :--- | :--- | :--- | :--- |
| **Planungsbedarf melden** (Bedarfsträger) → **Eingang bewerten** (Personalstelle) | **Reaktionszeit Planungsanfrage** | Zeitspanne bis zur ersten Bewertung des gemeldeten Planungsbedarfs durch die zentrale Stelle | < 2 Arbeitstage |
| **Eingangsdaten bereitstellen** (Bedarfsträger) → **Planungsdaten erfassen** (IT) | **Datenerfassungszeit** | Zeitaufwand für die strukturierte Erfassung und Validierung der bereitgestellten Eingangsdaten | < 3 Arbeitstage |
| **Daten konsolidieren** → **Bedarfsprognose berechnen** (IT) | **Berechnungszeit** | Dauer der automatisierten Berechnung der Bedarfsprognose (abhängig von Datenmenge und Komplexität) | < 4 Stunden (automatisiert) |
| **Auswertung bereitstellen** (IT) → **Ergebnis bewerten** (Personalstelle) | **Bewertungsdauer** | Zeitaufwand für die fachliche Bewertung und Plausibilisierung der IT-generierten Auswertung | < 5 Arbeitstage |
| **Planungsergebnis prüfen** (Bedarfsträger) → **Planungsergebnis freigeben** (Personalstelle) | **Freigabezyklus** | Zeitspanne zwischen Prüfung durch den Bedarfsträger und formaler Freigabe durch die Personalstelle | < 3 Arbeitstage |
| **Planungsergebnis freigeben** → **Planungsbericht veröffentlichen** | **Veröffentlichungszeit** | Zeit zwischen Freigabe und tatsächlicher Bereitstellung des finalen Berichts | < 1 Arbeitstag |

## Eingesetzte IT-Systeme
- **KM.Personal (Personalverwaltungssystem):** Lieferant für Bestandsdaten, Altersstruktur und historische Abgangszahlen als Basis für die Bedarfsprognose.
- **Strategisches Personalplanungs-Tool:** Spezialisierte Fachanwendung zur Erfassung, Konsolidierung und Berechnung der Personalbedarfsprognosen (z. B. auf Basis demografischer Modelle).
- **Business Intelligence (BI)-System:** Auswertung und Visualisierung der Planungskennzahlen (Dashboards, Trendanalysen, Szenarien).
- **DMS (Dokumentenmanagementsystem):** Revisionssichere Archivierung der Planungsberichte und Zwischenstände.
- **Intranet / Reporting-Portal:** Plattform zur Veröffentlichung der finalen Planungsberichte für Führungskräfte und Entscheidungsträger.

## Referenzdokumente
- BPMN-Modell: `Strategische_Personalbedarfsplanung_durchfuehren.bpmn`
- Personalstrategie "workSTUgether"
- Richtlinie zur strategischen Personalplanung
- Datenqualitätsstandards für Personalplanungsdaten
- Demografische Prognosemodelle und Berechnungsmethodik
