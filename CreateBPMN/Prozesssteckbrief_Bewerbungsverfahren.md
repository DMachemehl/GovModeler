# Prozesssteckbrief: Bewerbungsverfahren durchführen

## Zusammenfassung
Der Prozess **"Bewerbungsverfahren durchführen"** regelt die standardisierte Abwicklung von Recruiting-Vorgängen. Er beginnt mit der Meldung eines Personalbedarfs durch den Kunden, führt über die Beratung und Ausschreibung durch die Personalstellen zur Bewerberauswahl und endet mit der Kommunikation der Entscheidungen (inkl. Absageschreiben). Ziel ist eine effiziente, transparente und rechtssichere Stellenbesetzung unter Einbindung der zentralen und dezentralen Personalbereiche.

## Stammdaten
| Attribut | Wert |
| :--- | :--- |
| **Prozessname** | Bewerbungsverfahren durchführen |
| **Prozesskategorie** | Personal Recruiting |
| **Auslöser** | Personalbedarf ist entstanden und wurde gemeldet |
| **Ergebnis** | Bewerbungsverfahren abgeschlossen (Absageschreiben erteilt) |
| **Hauptverantwortung** | Personalstelle zentral |
| **Beteiligte Rollen** | Kunde (Führungskraft), Personalstelle dezentral, Personalstelle zentral |

## Prozessziele
1. **Effizienz:** Minimierung der Durchlaufzeiten (Time-to-Hire) durch zentralisierte Bearbeitung.
2. **Qualität:** Sicherstellung passgenauer Bewerberauswahlen durch strukturierte Anforderungsprofile.
3. **Rechtssicherheit:** Einhaltung aller gesetzlichen und tarifrechtlichen Vorgaben (AGG, etc.).
4. **Serviceorientierung:** Entlastung der Führungskräfte durch umfassenden Service der Personalstellen.

## Key Performance Indicators (KPIs)

Die folgenden Kennzahlen dienen der Messung der Prozessleistung und werden in Prozess-KPIs (Gesamtbetrachtung) und Aktivitäts-KPIs (Schrittbetrachtung) unterteilt.

### 1. Prozess-KPIs (Ebene Gesamtprozess)

Diese KPIs messen den Erfolg des gesamten End-to-End-Prozesses.

| KPI-ID | Kennzahl | Beschreibung | Zielwert | Messmethode |
| :--- | :--- | :--- | :--- | :--- |
| **P-KPI-01** | **Time-to-Hire (TTH)** | Gesamtzeitdauer vom Eingang der Personalbedarfsmeldung bis zum Abschluss des Verfahrens (Versand aller Schreiben). | < 60 Tage | `Timestamp(Endereignis) - Timestamp(Startereignis)` |
| **P-KPI-02** | **Prozessqualität** | Anteil der Verfahren ohne Rückfragen/Nachforderungen aufgrund unvollständiger Unterlagen. | > 90% | `Anzahl(Vorgänge ohne Loop) / Gesamtanzahl(Vorgänge)` |
| **P-KPI-03** | **Service-Level-Adherence** | Einhaltung der vereinbarten Service-Level-Agreements (SLA) über alle Prozessschritte hinweg. | > 95% | `Anzahl(Vorgänge in Time) / Gesamtanzahl(Vorgänge)` |

### 2. Aktivitäts-KPIs (Ebene Prozessschritte)

Diese KPIs sind spezifischen Aktivitäten oder Phasen im BPMN-Modell zugeordnet, um Engpässe zu identifizieren.

| Zugeordnete Aktivität(en) | KPI-Name | Beschreibung & Relevanz | Zielwert |
| :--- | :--- | :--- | :--- |
| **Personalbedarf melden** (Kunde) → **Anforderungsprofil freigeben** (Kunde) | **Dauer Bedarfsklärung** | Misst die Zeit, die benötigt wird, um das Anforderungsprofil final abzustimmen. Hohe Werte deuten auf Unklarheiten oder fehlende Beratung hin. | < 5 Werktage |
| **Bedarfsunterlagen erhalten** (PS zentral) → **Ausschreibung veröffentlichen** (PS zentral) | **Time-to-Publish** | Zeitdauer von der Übergabe an die zentrale Stelle bis zur Sichtbarkeit der Stelle. Kritisch für die schnelle Marktpräsenz. | < 3 Werktage |
| **Bewerbungen entgegennehmen** → **Bewerberauswahl durchführen** (PS zentral) | **Time-to-Shortlist** | Zeitdauer vom Bewerbungsschluss (oder Eingang) bis zur Vorlage der Kandidatenliste. Entscheidend für die Candidate Experience. | < 5 Werktage (nach Frist) |
| **Vorstellungsgespräche terminieren** → **Gesprächsergebnisse konsolidieren** | **Interview-Durchlaufzeit** | Dauer der Interviewphase inkl. Terminierung und Durchführung. Lange Phasen erhöhen das Absprungrisiko von Kandidaten. | < 10 Werktage |
| **Auswahlentscheidung übermitteln** (Kunde) → **Absageschreiben erteilen** (PS zentral) | **Reaktionsgeschwindigkeit Abschluss** | Zeit von der Entscheidung bis zur Kommunikation an die Bewerbenden. Wichtig für ein professionelles Employer Branding. | < 2 Werktage |

## Eingesetzte IT-Systeme
- **KM.Personal:** Führendes Personalverwaltungssystem (Stammdaten, Stellenplan).
- **Bewerbermanagement-System (BMS):** Verwaltung der Bewerbungseingänge und Kommunikation.
- **DMS (Dokumentenmanagement):** Archivierung der Verfahrensakten.

## Referenzdokumente
- BPMN-Modell: `Bewerbungsverfahren_durchfuehren.bpmn`
- Dienstvereinbarungen zum Auswahlverfahren
- AGG-Leitfaden
