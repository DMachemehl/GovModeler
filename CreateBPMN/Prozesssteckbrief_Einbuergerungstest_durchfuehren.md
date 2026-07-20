# Prozesssteckbrief: Einbürgerungstest durchführen

## Zusammenfassung
Der Prozess **"Einbürgerungstest durchführen"** umfasst die formale Abwicklung des standardisierten Einbürgerungstests, beginnend mit der elektronischen Anmeldung des Bürgers über die terminierte Durchführung bis hin zur Ausstellung und Übermittlung der Testbescheinigung. Ziel ist eine effiziente, transparente und rechtssichere Durchführung des Tests unter weitgehender Automatisierung von IT-gestützten Auswertungsschritten.

## Stammdaten
| Attribut | Wert |
| :--- | :--- |
| **Prozessname** | Einbürgerungstest durchführen |
| **Prozesskategorie** | Bürger (TOP 100) / Integration / Einbürgerung |
| **Auslöser** | Anmeldung zum Einbuergerungstest eingegangen |
| **Ergebnis** | Einbuergerungstest abgeschlossen |
| **Hauptverantwortung** | Einbürgerungsbehörde / VHS |
| **Beteiligte Rollen** | Bürger (Antragsteller), IT (System), Behörde (Prüfungsstelle) |

## Prozessziele
1. **Rechtssicherheit:** Sicherstellung einer ordnungsgemäßen Testdurchführung und validen Ergebnisermittlung gemäß den gesetzlichen Vorgaben.
2. **Effizienz:** Minimierung der administrativen Durchlaufzeiten durch automatisierte Testfragengenerierung und maschinelle Auswertung.
3. **Serviceorientierung:** Transparente Kommunikation und zeitnahe Terminvergabe für Bürger zur Förderung der Integration.
4. **Qualität:** Vermeidung von Erfassungs- und Auswertungsfehlern durch medienbruchfreie Datenverarbeitung und automatisierte Kontrollen.

## Key Performance Indicators (KPIs)

Die folgenden Kennzahlen dienen der Messung der Prozessleistung und werden in Prozess-KPIs (Gesamtbetrachtung) und Aktivitäts-KPIs (Schrittbetrachtung) unterteilt.

### 1. Prozess-KPIs (Ebene Gesamtprozess)

Diese KPIs messen den Erfolg des gesamten End-to-End-Prozesses.

| KPI-ID | Kennzahl | Beschreibung | Zielwert | Messmethode |
| :--- | :--- | :--- | :--- | :--- |
| **P-KPI-01** | **Time-to-Certificate (Durchlaufzeit)** | Gesamtdauer von der Testanmeldung bis zum Erhalt der Bescheinigung | < 4 Wochen | Timestamp(Bescheinigung erhalten) - Timestamp(Anmeldung eingegangen) |
| **P-KPI-02** | **Erfolgsquote** | Anteil der Teilnehmer, die den Test bestehen (mind. 17 Punkte) | > 80% | Anzahl(Bestanden) / Anzahl(Teilnehmer gesamt) |
| **P-KPI-03** | **Automatisierungsgrad** | Anteil der vollständig automatisiert ausgewerteten Tests (ohne manuellen Eingriff) | > 95% | Anzahl(Auto-Auswertung) / Anzahl(Gesamt) |
| **P-KPI-04** | **Terminverfügbarkeit** | Wartezeit bis zum nächstmöglichen freien Prüfungstermin | < 2 Wochen | Datum(Nächster freier Termin) - Datum(Heute) |

### 2. Aktivitäts-KPIs (Ebene Prozessschritte)

Diese KPIs sind spezifischen Aktivitäten oder Phasen im BPMN-Modell zugeordnet, um Engpässe zu identifizieren.

| Zugeordnete Aktivität(en) | KPI-Name | Beschreibung & Relevanz | Zielwert |
| :--- | :--- | :--- | :--- |
| **Testanmeldung einreichen** (Bürger) → **Testtermin vergeben** (Behörde) | **Time-to-Appointment** | Zeitdauer zwischen Anmeldungseingang und Terminvergabe. Relevant für die Servicequalität. | < 2 Werktage |
| **Testtermin vergeben** (Behörde) → **Testtermin wahrnehmen** (Bürger) | **Terminvorlaufzeit** | Zeit zwischen Terminvergabe und tatsächlicher Durchführung. Indikator für Planungshorizont. | 14-21 Tage |
| **Testtermin wahrnehmen** (Bürger) → **Testtermin wahrnehmen** (Bürger) | **No-Show-Rate** | Anteil der angemeldeten Teilnehmer, die nicht zum Termin erscheinen. Ressourcenauslastung. | < 10% |
| **Testbogen erfassen** (Behörde) → **Testergebnis auswerten** (IT) | **Erfassungsdauer** | Zeit für Übertragung der Antworten in das System. Engpassindikator bei manueller Erfassung. | < 1 Tag |
| **Testfragen generieren** (IT) → **Testbogen erhalten** (IT) | **Systemverfügbarkeit Testabruf** | Latenzzeit bei der Bereitstellung personalisierter Testbögen. Kritisch für Testbeginn. | < 30 Sekunden |
| **Testergebnis erhalten** (Behörde) → **Bescheinigung ausstellen** (Behörde) | **Bearbeitungszeit Bescheinigung** | Zeitdauer vom Vorliegen des Ergebnisses bis zur Ausfertigung der Urkunde. | < 1 Werktag |

## Eingesetzte IT-Systeme
- **Fachverfahren Einbürgerung (FEIN):** Zentrales System zur Verwaltung von Einbürgerungsvorgängen und Terminmanagement.
- **Fragenkatalog-Datenbank:** System zur Zufallsgenerierung von Testfragen aus dem bundesweiten Pool.
- **Auswertungs-Engine:** Automatisierte Routine zur Korrektur von Multiple-Choice-Antworten und Punkteberechnung.

## Referenzdokumente
- BPMN-Modell: `CreateBPMN/Einbuergerungstest_durchfuehren.bpmn`
- Staatsangehörigkeitsgesetz (StAG)
- Einbürgerungstestverordnung (EinbTestV)
- Verordnung zu Einbürgerungstest und Einbürgerungskurs (EinbTestEntgV)
