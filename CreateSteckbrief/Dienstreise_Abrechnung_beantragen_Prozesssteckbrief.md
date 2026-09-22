# Prozesssteckbrief: Abrechnung einer Dienstreise beantragen

## Zusammenfassung
Der Prozess **"Abrechnung einer Dienstreise beantragen"** regelt das Verfahren zur Beantragung und Erstattung von Reisekosten nach Durchfuehrung einer dienstlichen Reise durch Beschaeftigte der Verwaltung. Er beginnt mit der Erfassung und Vorbereitung der Reisekostenabrechnung durch den Antragsteller, fuehrt ueber die digitale Eingangserfassung und automatisierte Vollstaendigkeitspruefung durch das IT-System sowie die fachliche Pruefung und Freigabe durch die zustaendige Reisekostenstelle und endet mit der automatisierten Auszahlung und der digitalen Bereitstellung des Erstattungsbescheids. Ziel ist eine effiziente, medienbruchfreie, transparente und rechtssichere Abwicklung aller Reisekostenerstattungen.

## Stammdaten
| Attribut | Wert |
| :--- | :--- |
| **Prozessname** | Abrechnung einer Dienstreise beantragen |
| **Prozesskategorie** | Personaladministration / Reisekostenmanagement / Finanzwesen |
| **Ausloeser** | Dienstreise durchgefuehrt |
| **Ergebnis** | Reisekostenabrechnung abgeschlossen |
| **Hauptverantwortung** | Personalstelle / Reisekostenstelle (zentral/dezentral) |
| **Beteiligte Rollen** | Buerger (Antragsteller / Beschaeftigter), IT (digitales Abrechnungssystem), Behoerde (Reisekostenstelle / Sachbearbeitung) |

## Prozessziele
1. **Effizienz:** Beschleunigung des Abrechnungsverfahrens durch volldigitale Belegerfassung, automatisierte Vorpruefung und strukturierte Uebermittlung an das Abrechnungssystem.
2. **Qualitaet:** Erhoehung der Abrechnungsqualitaet und Vermeidung von Rueckfragen durch gefuehrte Datenerfassung und automatisierte Pruefung von Pflichtangaben und Belegen.
3. **Rechtssicherheit:** Konsequente Einhaltung der gesetzlichen Bestimmungen (BRKG/LRKG) sowie interner Richtlinien zur Erstattungsfaehigkeit von Reiseaufwaenden.
4. **Serviceorientierung:** Anwenderfreundliche und transparente Abwicklung fuer Mitarbeitende mit kurzen Wartezeiten bis zur Erstattung.
5. **Transparenz:** Nachvollziehbare Dokumentation aller Pruef- und Freigabeschritte sowie jederzeit einsehbarer Bearbeitungsstatus.

## Key Performance Indicators (KPIs)

Die folgenden Kennzahlen dienen der Messung der Prozessleistung und werden in Prozess-KPIs (Gesamtbetrachtung) und Aktivitaets-KPIs (Schrittbetrachtung) unterteilt.

### 1. Prozess-KPIs (Ebene Gesamtprozess)

Diese KPIs messen den Erfolg des gesamten End-to-End-Prozesses.

| KPI-ID | Kennzahl | Beschreibung | Zielwert | Messmethode |
| :--- | :--- | :--- | :--- | :--- |
| **P-KPI-01** | **Gesamtdurchlaufzeit (End-to-End)** | Zeitdauer von der Antragsabgabe durch den Beschaeftigten bis zur Auszahlung und Bereitstellung des Erstattungsbescheids. | < 5 Arbeitstage | Timestamp(Erstattungsbescheid bereitgestellt) - Timestamp(Antrag eingereicht) |
| **P-KPI-02** | **First-Pass-Yield (FPY)** | Anteil der Reisekostenantraege, die ohne manuelle Nachforderungen oder Rueckfragen direkt genehmigt und abgerechnet werden. | > 85% | Anzahl(Antraege ohne Rueckfrage) / Gesamtanzahl(Antraege) |
| **P-KPI-03** | **Service-Level-Einhaltung** | Einhaltung der vorgegebenen Bearbeitungsfrist fuer Reisekostenabrechnungen. | > 95% | Anzahl(fristgerecht bearbeitete Antraege) / Gesamtanzahl(Antraege) |
| **P-KPI-04** | **Digitalisierungsgrad** | Anteil der Reisekostenabrechnungen, die durchgaengig papierlos und ohne Medienbruch verarbeitet werden. | > 98% | Anzahl(volldigitale Abrechnungen) / Gesamtanzahl(Abrechnungen) |

### 2. Aktivitaets-KPIs (Ebene Prozessschritte)

Diese KPIs sind spezifischen Aktivitaeten oder Phasen im BPMN-Modell zugeordnet, um Engpaesse zu identifizieren.

| Zugeordnete Aktivitaet(en) | KPI-Name | Beschreibung & Relevanz | Zielwert |
| :--- | :--- | :--- | :--- |
| **Reisekostenabrechnung vorbereiten** (Buerger) → **Reisekostenantrag einreichen** (Buerger) | **Erfassungsdauer Antragsteller** | Zeitspanne vom Start der Belegerfassung bis zum finalen Absenden des Antrags. Indikator fuer Bedienerfreundlichkeit des Portals. | < 2 Arbeitstage nach Reiseende |
| **Antrag erfassen** (IT) → **Vollstaendigkeit pruefen** (IT) | **Automatische Pruefzeit** | Dauer der automatisierten Daten- und Belegpruefung durch das System. Engpassindikator fuer die Systemleistung. | < 1 Minute |
| **Vollstaendigkeit pruefen** (IT) → **Antragsdaten uebermitteln** (IT) | **IT-Weiterleitungszeit** | Zeitdauer zur Bereitstellung der geprueften Antragsdaten im Bearbeitungspool der Reisekostenstelle. | < 15 Minuten |
| **Antragsdaten uebermitteln** (IT) → **Zustaendigkeit pruefen** (Behoerde) | **Liegezeit bis Sachbearbeitung** | Wartezeit der Antragsdaten in der Eingangs-Queue der Behoerde bis zur Aufnahme der Bearbeitung. | < 1 Arbeitstag |
| **Zustaendigkeit pruefen** (Behoerde) → **Reisekostenrichtlinien anwenden** (Behoerde) | **Zustaendigkeitspruefungszeit** | Zeitbedarf zur Pruefung der sachlichen Zustaendigkeit und organisatorischen Zuordnung. | < 2 Stunden |
| **Reisekostenrichtlinien anwenden** (Behoerde) → **Erstattungsbetrag festlegen** (Behoerde) | **Fachpruefungsdauer** | Bearbeitungszeit fuer die materielle Pruefung von Belegen, Wegstrecken und Pauschalen gemaess Reisekostenrecht. | < 1 Arbeitstag |
| **Erstattungsbetrag festlegen** (Behoerde) → **Freigabe erteilen** (Behoerde) | **Freigabezeit** | Zeitspanne fuer die Festlegung des Erstattungsbetrags und die rechnerische/sachliche Freigabe. | < 4 Stunden |
| **Erstattung auszahlen** (IT) → **Erstattungsbescheid bereitstellen** (IT) | **Auszahlungs- und Bescheidbereitstellungszeit** | Zeitdauer zwischen technischer Auszahlungsanweisung im ERP-/Finanzsystem und Bereitstellung des Bescheids. | < 1 Arbeitstag |

## Eingesetzte IT-Systeme
- **Mitarbeiterportal / Reisekostenportal:** Webbasierte Oberflaeche zur digitalen Erfassung von Reisedaten, Hochladen von Belegen und Einreichen des Reisekostenantrags.
- **Workflow- & Antragsmanagementsystem:** Steuerung des automatisierten Pruef-, Uebermittlungs- und Freigabeprozesses ueber Schnittstellen hinweg.
- **ERP- & Finanzsystem (z.B. SAP / KM.Personal):** Fachanwendung zur Berechnung der Erstattungsbetraege, Fuehrung der Buchungsdaten und Ausfuehrung des Zahllaufs.
- **DMS (Dokumentenmanagementsystem):** Revisionssichere Archivierung der digitalen Abrechnungsunterlagen, Belege und Bescheide.
- **Output-Management-System:** Erstellung und digitale Zustellung des Erstattungsbescheids in das Postfach des Mitarbeitenden.

## Referenzdokumente
- BPMN-Modell: `Dienstreise_Abrechnung_beantragen.bpmn`
- Formular: `Reisekostenantrag_einreichen.form`
- Bundesreisekostengesetz (BRKG) bzw. Landesreisekostengesetz (LRKG)
- Allgemeine Verwaltungsvorschrift zum Bundesreisekostengesetz (BRKGVwV)
- Interne Dienstvereinbarungen und Reiserichtlinien zur Genehmigung und Abrechnung von Dienstreisen
