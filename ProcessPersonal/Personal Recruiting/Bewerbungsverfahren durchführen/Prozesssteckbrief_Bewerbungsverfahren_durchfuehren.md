# Prozesssteckbrief: Bewerbungsverfahren durchführen

## Zusammenfassung
Der Prozess **"Bewerbungsverfahren durchführen"** steuert die Durchführung von Recruiting-Maßnahmen von der Bedarfsmeldung bis zum Verfahrensabschluss. Beginnend mit der Meldung eines Personalbedarfs durch den Fachbereich, führt der Prozess über die Ausschreibungserstellung und -veröffentlichung sowie die strukturierte Bewerbervorauswahl und Interviewführung bis zur Auswahlentscheidung und abschließenden Bescheidung aller Bewerbenden. Ziel ist die effiziente und rechtssichere Besetzung vakanter Stellen unter optimaler Einbindung der zentralen und dezentralen Personalstellen sowie der Führungskräfte.

## Stammdaten
| Attribut | Wert |
| :--- | :--- |
| **Prozessname** | Bewerbungsverfahren durchführen |
| **Prozesskategorie** | Personal Recruiting |
| **Auslöser** | Personalbedarf ist gemeldet worden |
| **Ergebnis** | Absageschreiben sind erteilt worden / Auswahlentscheidung ist getroffen |
| **Hauptverantwortung** | Personalstelle zentral (Verfahrensführung), Personalstelle dezentral (Beratung), Kunde (fachl. Entscheidung) |
| **Beteiligte Rollen** | Kunde (Fachbereich), Personalstelle dezentral, Personalstelle zentral |

## Prozessziele
1. **Qualität & Passgenauigkeit:** Sicherstellung einer qualifizierten Bewerberauswahl durch strukturierte Vorprüfungs- und Interviewprozesse zur Besetzung mit dem bestmöglichen Kandidaten.
2. **Effizienz (Time-to-Hire):** Minimierung der Vakanzzeiten durch optimierte Durchlaufzeiten und klare Verantwortlichkeiten zwischen Fachbereich und Personalstellen.
3. **Rechtssicherheit & Compliance:** Gewährleistung eines diskriminierungsfreien Verfahrens gemäß AGG und Einhaltung interner Richtlinien (Bestenauslese).
4. **Serviceorientierung:** Entlastung der Fachbereiche von administrativen Aufgaben durch zentrale Services (Ausschreibung, Kommunikation, Organisation).

## Key Performance Indicators (KPIs)

Die folgenden Kennzahlen dienen der Messung der Prozessleistung und werden in Prozess-KPIs (Gesamtbetrachtung) und Aktivitäts-KPIs (Schrittbetrachtung) unterteilt.

### 1. Prozess-KPIs (Ebene Gesamtprozess)

Diese KPIs messen den Erfolg des gesamten End-to-End-Prozesses.

| KPI-ID | Kennzahl | Beschreibung | Zielwert | Messmethode |
| :--- | :--- | :--- | :--- | :--- |
| **P-KPI-01** | **Time-to-Hire (Gesamt)** | Gesamtdauer vom Eingang der vollständigen Bedarfsmeldung bis zur finalen Auswahlentscheidung. Misst die Geschwindigkeit der Stellenbesetzung. | < 45 Tage | Timestamp(Auswahlentscheidung) - Timestamp(Bedarfsmeldung) |
| **P-KPI-02** | **Verfahrenseffizienz** | Anteil erfolgreich abgeschlossener Verfahren im Verhältnis zu abgebrochenen Verfahren (z.B. mangels geeigneter Bewerber). | > 90% | Anzahl(Erfolgreiche Besetzungen) / Gesamtanzahl(Verfahren) |
| **P-KPI-03** | **Service-Quality Score** | Zufriedenheit der Fachbereiche mit der Serviceleistung der Personalstellen (aktive Unterstützung, Qualität der Bewerberlisten). | > 4.5 / 5.0 | Jährliche Zufriedenheitsbefragung der Führungskräfte |
| **P-KPI-04** | **Bewerber-Response-Rate** | Durchschnittliche Zeit bis zur ersten persönlichen Rückmeldung an Bewerbende (Eingangsbestätigung/Statusupdate) nach Bewerbungseingang. | < 2 Werktage | Durchschnitt(Timestamp(Erste Antwort) - Timestamp(Bewerbungseingang)) |

### 2. Aktivitäts-KPIs (Ebene Prozessschritte)

Diese KPIs sind spezifischen Aktivitäten oder Phasen im BPMN-Modell zugeordnet, um Engpässe zu identifizieren.

| Zugeordnete Aktivität(en) | KPI-Name | Beschreibung & Relevanz | Zielwert |
| :--- | :--- | :--- | :--- |
| **Personalbedarf melden** (Kunde) → **Ausschreibung bereitstellen** (Personal zentral) | **Time-to-Draft** | Zeitspanne von der Bedarfsmeldung bis zur Bereitstellung des fertigen Ausschreibungsentwurfs zur Freigabe. Prüft die initiale Reaktionsgeschwindigkeit. | < 5 Werktage |
| **Ausschreibung freigeben** (Kunde) → **Ausschreibung veröffentlichen** (Personal zentral) | **Time-to-Publish** | Zeitverzögerung zwischen fachlicher Freigabe und tatsächlicher Veröffentlichung der Stelle. Relevant für schnelle Marktpräsenz. | < 2 Werktage |
| **Bewerbungen entgegennehmen** → **Übersicht bereitstellen** (Personal zentral) | **Screening-Duration** | Zeitaufwand für die Sichtung, Vorprüfung und Aufbereitung der Bewerbungsunterlagen nach Fristende. Engpass für den weiteren Verlauf. | < 3 Werktage (nach Fristende) |
| **Übersicht bereitstellen** (Personal zentral) → **Bewerberauswahl festlegen** (Kunde) | **Decision-Time (Shortlist)** | Zeit, die der Fachbereich benötigt, um aus der Liste die Kandidaten für Gespräche auszuwählen. Indikator für Verzögerungen im Fachbereich. | < 5 Werktage |
| **Vorstellungsgespräche führen** (Kunde) → **Auswahlentscheidung übermitteln** (Kunde) | **Decision-Time (Interview)** | Zeitspanne zwischen den geführten Gesprächen und der finalen Entscheidungsmeldung an das Personalmanagement. | < 3 Werktage |
| **Auswahlentscheidung mitteilen** (Kunde) → **Absageschreiben erteilen** (Personal zentral) | **Closing-Time** | Zeitdauer bis zum formalen Abschluss des Verfahrens für abgelehnte Bewerber. Relevant für Employer Branding und Fairness. | < 5 Werktage |

## Eingesetzte IT-Systeme
- **Bewerbermanagement-System (BMS):** Zentrales System zur Erfassung von Bewerbungen, Kommunikation mit Kandidaten und Prozesssteuerung.
- **KM.Personal / SAP HCM:** Stammdatenführendes System für Personalbedarfsplanung und Anlage neuer Mitarbeiterdaten.
- **Inter-Amt-Portal / Website:** Veröffentlichungsplattformen für Stellenausschreibungen.
- **DMS (Dokumentenmanagement):** Archivierung der Verfahrensakten und revisionssichere Ablage der Auswahlentscheidungen.

## Referenzdokumente
- BPMN-Modell: `CreateBPMN/Bewerbungsverfahren_durchfuehren.bpmn`
- Allgemeines Gleichbehandlungsgesetz (AGG)
- Interne Richtlinie zur Personalauswahl und Stellenausschreibung
- Dienstvereinbarung zum Bewerbungsmanagement
