# Prozesssteckbrief: Beschäftigungsverhältnis/Dienstverhältnis begründen (Einstellung)

## Zusammenfassung
Der Prozess **"Beschäftigungsverhältnis/Dienstverhältnis begründen (Einstellung)"** beschreibt die administrative Umsetzung einer Neueinstellung nach Abschluss des Auswahlverfahrens. Er beginnt mit der Übermittlung des Einstellungsauftrags durch den Kunden, führt über die Beteiligung des Personalrats, die Vertragserstellung und die Erfassung der Stammdaten in den HR-Systemen bis hin zur abschließenden Vorbereitung des Onboardings (Voraberfassung). Ziel ist die rechtssichere Vertragsgestaltung und die Sicherstellung der Arbeitsfähigkeit des neuen Mitarbeitenden zum ersten Arbeitstag.

## Stammdaten
| Attribut | Wert |
| :--- | :--- |
| **Prozessname** | Beschäftigungsverhältnis/Dienstverhältnis begründen (Einstellung) |
| **Prozesskategorie** | Personal Recruiting |
| **Auslöser** | Einstellungsbedarf bestätigt (Auswahlentscheidung getroffen) |
| **Ergebnis** | Beschäftigungsverhältnis administrativ begründet (Eintritt vorbereitet) |
| **Hauptverantwortung** | Personalstelle zentral |
| **Beteiligte Rollen** | Kunde (Führungskraft/Beschäftigter), Personalstelle dezentral, Personalstelle zentral |

## Prozessziele
1. **Rechtssicherheit:** Gewährleistung rechtlich einwandfreier Arbeitsverträge und Ernennungen unter Einhaltung aller gesetzlichen und tarifrechtlichen Vorgaben (z.B. TVöD, LBG).
2. **Effizienz & Schnelligkeit:** Minimierung der administrativen Durchlaufzeit, um Bewerber kurzfristig zu binden und Vakanzen schnell zu besetzen.
3. **Datenqualität:** Sicherstellung korrekter und vollständiger Stammdaten im HR-System (KM.Personal) als Basis für die Entgeltabrechnung ("First-Time-Right").
4. **Serviceorientierung:** Transparenter und unterstützender Prozess für die neue Führungskraft und den neuen Mitarbeitenden zur Förderung einer positiven "Candidate Experience" und eines gelungenen Onboardings.

## Key Performance Indicators (KPIs)

Die folgenden Kennzahlen dienen der Messung der Prozessleistung und werden in Prozess-KPIs (Gesamtbetrachtung) und Aktivitäts-KPIs (Schrittbetrachtung) unterteilt.

### 1. Prozess-KPIs (Ebene Gesamtprozess)

Diese KPIs messen den Erfolg des gesamten End-to-End-Prozesses.

| KPI-ID | Kennzahl | Beschreibung | Zielwert | Messmethode |
| :--- | :--- | :--- | :--- | :--- |
| **P-KPI-01** | **Time-to-Hire (Admin)** | Gesamtdauer vom Eingang des Einstellungsauftrags bis zur abgeschlossenen Voraberfassung | < 10 Arbeitstage | Timestamp(Eintritt bearbeitet) - Timestamp(Auftrag eingegangen) |
| **P-KPI-02** | **Vertragsqualität** | Anteil der Arbeitsverträge, die ohne nachträgliche Korrektur unterschrieben zurückkommen | > 98% | (Anzahl Verträge ohne Korrektur / Gesamtanzahl Verträge) * 100 |
| **P-KPI-03** | **Onboarding-Readiness** | Anteil der Fälle, bei denen alle technischen Ressourcen (Account, Hardware) vor Tag 1 beantragt wurden | 100% | Anzahl(IT-Anforderungen vor Startdatum) / Gesamtanzahl Einstellungen |
| **P-KPI-04** | **Stammdatenqualität** | Fehlerquote bei der ersten Gehaltsabrechnung aufgrund falscher Stammdatenerfassung | < 1% | Anzahl(Korrekturbuchungen Monat 1) / Gesamtanzahl Neueinstellungen |

### 2. Aktivitäts-KPIs (Ebene Prozessschritte)

Diese KPIs sind spezifischen Aktivitäten oder Phasen im BPMN-Modell zugeordnet, um Engpässe zu identifizieren.

| Zugeordnete Aktivität(en) | KPI-Name | Beschreibung & Relevanz | Zielwert |
| :--- | :--- | :--- | :--- |
| **[Kundenberatung]** (PS dezentral) → **[Einstellungsinfo konsolidieren]** (PS dezentral) | **Beratungs-Durchlaufzeit** | Dauer der initialen Klärung und Aufbereitung der Daten durch die dezentrale Stelle. Relevant für die Qualität des Inputs an die zentrale Stelle. | < 2 Arbeitstage |
| **[Zuständigkeit prüfen]** (PS zentral) → **[Vollständigkeit prüfen]** (PS zentral) | **Reaktionszeit Eingang** | Zeitdauer bis zur ersten qualifizierten Bearbeitung durch die zentrale Stelle nach Eingang der Daten. | < 4 Stunden |
| **[Personalratsbeteiligung einleiten]** → **[Vertragskonditionen finalisieren]** | **PR-Laufzeit** | Zeitdauer für die Zustimmung des Personalrats. Dies ist oft ein externer Flaschenhals ("Wartezeit"). | < 7 Kalendertage |
| **[Vertragskonditionen finalisieren]** → **[Einstellungsunterlagen versenden]** | **Erstellungsdauer Vertrag** | Zeitdauer für die physische Erstellung und den Versand des Vertrags nach Vorliegen aller Genehmigungen. | < 2 Arbeitstage |
| **[Einstellungsunterlagen versenden]** → **[Ausgefüllte Unterlagen erhalten]** | **Rücklaufzeit Kandidat** | Zeitdauer, die der Bewerber für die Unterschrift benötigt. Indikator für Verbindlichkeit und Postlaufzeiten. | < 5 Arbeitstage |
| **[Gehaltsrelevante Unterlagen verarbeiten]** → **[Voraberfassung durchführen]** | **Erfassungsgeschwindigkeit** | Zeitdauer für die Übertragung der Papierdaten in das HR-System. Relevant für Abrechnungstermine. | < 1 Arbeitstag |

## Eingesetzte IT-Systeme
- **KM.Personal:** SAP-basiertes Personalwirtschaftssystem zur Pflege der Stammdaten, Verwaltung der Stellenpläne und Durchführung der Entgeltabrechnung (einschließlich "Time Manager's Workplace").
- **DMS (Dokumentenmanagement):** Elektronische Personalakte zur rechtssicheren Ablage aller vertragsrelevanten Dokumente.
- **Office-Anwendungen:** Erstellung von Arbeitsverträgen und Schriftverkehr basierend auf Vorlagen.

## Referenzdokumente
- BPMN-Modell: `CreateBPMN/Beschaeftigungsverhaeltnis_begruenden_Einstellung.bpmn`
- Tarifvertrag für den öffentlichen Dienst (TVöD)
- Landesbeamtengesetz (LBG)
- Dienstvereinbarungen zu Einstellungsprozessen
- Onboarding-Leitfaden für Führungskräfte

