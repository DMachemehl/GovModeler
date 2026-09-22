# Prozesssteckbrief: Anmeldung zur berufsbildenden Schule bearbeiten

## Zusammenfassung
Der Prozess **"Anmeldung zur berufsbildenden Schule bearbeiten"** dient dazu, die Anmeldung einer buergerlichen Person an einer berufsbildenden Schule rechtssicher zu pruefen und ueber die Zuweisung eines Schulplatzes zu entscheiden. Der Prozess beginnt mit dem Eingang der Anmeldung beim Schulverwaltungsamt, fuehrt ueber die digitale Pruefung von Vollstaendigkeit und Schulplatzverfuegbarkeit im IT-System sowie die fachliche Zuweisung durch das Schulverwaltungsamt zur Erstellung und Zustellung des Bescheids. Ziel ist eine effiziente, transparente und rechtssichere Bearbeitung der Anmeldung unter Einbindung der beteiligten Stellen.

## Stammdaten
| Attribut | Wert |
| :--- | :--- |
| **Prozessname** | Anmeldung zur berufsbildenden Schule bearbeiten |
| **Prozesskategorie** | Bildung, Schulverwaltung |
| **Auslöser** | Anmeldung eingegangen |
| **Ergebnis** | Bescheid zugestellt |
| **Hauptverantwortung** | Schulverwaltungsamt |
| **Beteiligte Rollen** | Buerger, IT, Schulverwaltungsamt |

## Prozessziele
1. **Effizienz:** Minimierung der Durchlaufzeit zwischen Anmeldeeingang und Bescheiderteilung durch automatisierte IT-Pruefschritte.
2. **Qualitaet:** Sicherstellung einer korrekten Pruefung von Vollstaendigkeit und Schulplatzverfuegbarkeit, um Fehlzuweisungen zu vermeiden.
3. **Rechtssicherheit:** Zuweisung der Schulplaetze gemaess den geltenden Zulassungs- und Kapazitaetsvorgaben.
4. **Serviceorientierung:** Ermoeglichung einer einfachen und transparenten digitalen Anmeldung fuer den Buerger.
5. **Automatisierung:** Vollautomatisierte Durchfuehrung der Datenerfassungs- und Pruefschritte im IT-System.

## Key Performance Indicators (KPIs)

Die folgenden Kennzahlen dienen der Messung der Prozessleistung und werden in Prozess-KPIs (Gesamtbetrachtung) und Aktivitäts-KPIs (Schrittbetrachtung) unterteilt.

### 1. Prozess-KPIs (Ebene Gesamtprozess)

Diese KPIs messen den Erfolg des gesamten End-to-End-Prozesses.

| KPI-ID | Kennzahl | Beschreibung | Zielwert | Messmethode |
| :--- | :--- | :--- | :--- | :--- |
| **P-KPI-01** | **Gesamtdurchlaufzeit** | Misst die Zeit vom Eingang der Anmeldung bis zur Zustellung des Bescheids. | < 10 Arbeitstage | Timestamp(EndEvent_Behoerde) - Timestamp(StartEvent_Antrag_eingegangen) |
| **P-KPI-02** | **Erst-Erfolgs-Rate** | Anteil der Anmeldungen, die ohne Nachforderung von Unterlagen vollstaendig bearbeitet werden koennen. | > 95% | (Anzahl fehlerfreie Anmeldungen / Gesamtanzahl Anmeldungen) * 100 |
| **P-KPI-03** | **Service-Level** | Anteil der Anmeldungen, deren Bescheid innerhalb der Zielfrist zugestellt wird. | > 90% | Anzahl(Bescheid fristgerecht) / Gesamtanzahl Anmeldungen |
| **P-KPI-04** | **Automatisierungsgrad** | Anteil der vollautomatisierten Pruefschritte im IT-Prozess (Erfassen, Vollstaendigkeit, Schulplatzverfuegbarkeit). | 100% | Anzahl(automatisierte IT-Tasks) / Anzahl(gesamte IT-Tasks) |

### 2. Aktivitäts-KPIs (Ebene Prozessschritte)

Diese KPIs sind spezifischen Aktivitäten oder Phasen im BPMN-Modell zugeordnet, um Engpässe zu identifizieren.

| Zugeordnete Aktivität(en) | KPI-Name | Beschreibung & Relevanz | Zielwert |
| :--- | :--- | :--- | :--- |
| **Task_Anmeldeformular_ausfuellen** (Buerger) → **Task_Anmeldung_einreichen** (Buerger) | **Ausfuelldauer** | Zeit, die der Buerger zum Ausfuellen und Einreichen des Anmeldeformulars benoetigt. Indikator fuer die Benutzerfreundlichkeit des Formulars. | < 15 Minuten |
| **Task_Anmeldung_einreichen** (Buerger) → **StartEvent_Antrag_eingegangen** (Schulverwaltungsamt) | **Uebermittlungsdauer** | Zeit fuer die technische Uebermittlung der Anmeldung vom Buerger-Frontend zum Schulverwaltungsamt. | < 5 Sekunden |
| **Task_Zustaendigkeit_pruefen** (Schulverwaltungsamt) → **Task_Anmeldedaten_uebermitteln** (Schulverwaltungsamt) | **Pruefzeit Zustaendigkeit** | Zeit fuer die Feststellung der fachlichen Zustaendigkeit, bevor die Daten an die IT uebermittelt werden. | < 1 Arbeitstag |
| **Task_Anmeldedaten_erfassen** (IT) → **Task_Pruefergebnis_bereitstellen** (IT) | **IT-Verarbeitungszeit** | Misst die reine Verarbeitungszeit des IT-Systems von der Datenerfassung bis zur Bereitstellung des Pruefergebnisses. | < 30 Sekunden |
| **Task_Anmeldedaten_uebermitteln** (Schulverwaltungsamt) → **Event_Pruefergebnis_erhalten** (Schulverwaltungsamt) | **Wartezeit auf IT-Pruefergebnis** | Wartezeit des Schulverwaltungsamts auf die Rueckmeldung des IT-Systems. Indikator fuer die IT-Antwortzeit. | < 1 Stunde |
| **Event_Pruefergebnis_erhalten** (Schulverwaltungsamt) → **Task_Schulplatz_zuweisen** (Schulverwaltungsamt) | **Entscheidungszeit Schulplatzzuweisung** | Zeit fuer die fachliche Entscheidung zur Zuweisung des Schulplatzes auf Basis des Pruefergebnisses. | < 2 Arbeitstage |
| **Task_Schulplatz_zuweisen** (Schulverwaltungsamt) → **Task_Bescheid_erstellen** (Schulverwaltungsamt) | **Bescheiderstellungsdauer** | Zeit zur Erstellung des Bescheids nach erfolgter Schulplatzzuweisung. | < 1 Arbeitstag |
| **Task_Bescheid_erstellen** (Schulverwaltungsamt) → **Event_Bescheid_erhalten** (Buerger) | **Zustelldauer Bescheid** | Zeit fuer die Zustellung des Bescheids an den Buerger nach Erstellung. | < 2 Arbeitstage |

## Eingesetzte IT-Systeme
- **Schulverwaltungssystem:** Fachverfahren zur Erfassung der Anmeldedaten, Pruefung der Vollstaendigkeit und Abgleich der Schulplatzverfuegbarkeit.
- **Online-Anmeldeportal:** Web-Frontend, ueber das Buerger die Anmeldung digital einreichen und den Bescheid empfangen koennen.

## Referenzdokumente
- BPMN-Modell: `Anmeldung_zur_berufsbildenden_Schule_bearbeiten.bpmn`
- Formular: `Anmeldung_zur_berufsbildenden_Schule_Antrag.form`
- Schulgesetz und Schulordnung des jeweiligen Bundeslandes (Zulassungs- und Kapazitaetsvorgaben)

---
