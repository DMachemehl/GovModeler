# Prozesssteckbrief: TP4 Medien einarbeiten

## Zusammenfassung
Der Prozess **„TP4 Medien einarbeiten"** umfasst alle Arbeitsschritte, die nach dem physischen Eingang eines gelieferten Mediums bis zu seiner Ausleihbereitschaft notwendig sind. Er beginnt mit der Lieferkontrolle durch die FaMIs und führt über Inventarisierung, Rechnungsbegleichung, vollständige Katalogisierung (Formal- und Sacherschließung in aDIS/BMS), technische Einarbeitung (Signatur, Folie, RFID) bis zur abschließenden Freischaltung für die Ausleihe. Der Prozess endet mit einem ausleihfertigen Medium, dessen Bereitstellungsbenachrichtigung bei Vorbestellungen automatisch ausgelöst wird. Ziel ist eine fehlerfreie, normkonforme Einarbeitung und schnellstmögliche Bereitstellung für die Bibliotheksnutzer:innen.

## Stammdaten
| Attribut | Wert |
| :--- | :--- |
| **Prozessname** | TP4 Medien einarbeiten |
| **Übergeordneter Prozess** | Medienbestand managen – Stadtbibliothek Stuttgart |
| **Prozesskategorie** | Bibliotheksmanagement / Medienbestandsmanagement |
| **Auslöser** | Medium geliefert und Einarbeitung beauftragt |
| **Ergebnis** | Medium ist ausleihfertig und Bereitstellung ist erfolgt |
| **Hauptverantwortung** | FaMIs (Fachangestellte für Medien- und Informationsdienste) |
| **Beteiligte Rollen** | FaMIs, Bibliotheksnutzer (Kunde) |
| **Supplier** | Medienlieferanten (physische Lieferung), 41-3 HV Hauptverwaltung (Rechnungsbearbeitung), Fremddatenanbieter / Fachdatenbanken (Katalogdaten) |
| **Vorgelagerter Prozess** | TP3 Medien erwerben |
| **Nachgelagerte Prozesse** | TP5 Medien vermitteln, TP6 Bestand pflegen |
| **BPMN-Modell** | Bibliothek_Medienbestand_TP4_Medien_einarbeiten.bpmn |

## Prozessziele
1. **Schnelligkeit:** Minimierung der Zeitspanne zwischen Liefereingang und Ausleihbereitschaft zur raschen Erfüllung von Vorbestellungen.
2. **Datenqualität:** Vollständige und normengerechte Katalogisierung (Formal- und Sacherschließung) als Grundlage für die Auffindbarkeit im OPAC.
3. **Physische Qualität:** Fachgerechte technische Einarbeitung (Signatur, Schutzfolie, RFID) nach medientypspezifischen Standards der Stadtbibliothek Stuttgart.
4. **Finanzkonformität:** Revisionssichere Rechnungsbegleichung und Etatbuchung über SAP/aDIS.
5. **Serviceorientierung:** Automatische Bereitstellungsbenachrichtigung bei bestehenden Vorbestellungen unmittelbar nach Freischaltung.

## Detaillierte Prozessschritte

### Pool: Kunde (Bibliotheksnutzer / Bürger)

| Nr. | Schritt | Beschreibung |
| :--- | :--- | :--- |
| K1 | **Vorbestellung aufgeben** | Der Bürger gibt im OPAC (aDIS/WebOPAC) eine Vormerkung auf das bestellte, noch nicht eingearbeitete Medium auf. Die Vormerkung ist möglich, sobald das Medium nach der Inventarisierung (Schritt O2) im System als „vorbestellbar" markiert ist. |
| K2 | **Bereitstellungsbenachrichtigung empfangen** | Nach der Freischaltung des Mediums (Schritt O6 – Freibuchen) erhält der Bürger automatisch eine Bereitstellungsbenachrichtigung über den OPAC oder per Nachricht. Die Vorbestellung wird zur Abholung bereitgelegt. |

### Pool: Organisation

| Nr. | Rolle/Lane | Schritt | Beschreibung |
| :--- | :--- | :--- | :--- |
| O1 | FaMIs | **Lieferkontrolle durchführen** | Die FaMIs prüfen die eingegangene Lieferung gegen den Bestelldatensatz in aDIS/BMS: Vollständigkeit, Zustand der Medien, Übereinstimmung von Titel, ISBN und Exemplaranzahl. Mangelhafte oder falsch gelieferte Medien werden für die Reklamation gesondert markiert. |
| O2 | FaMIs | **Medium inventarisieren** | Die FaMIs inventarisieren jedes Medium manuell (Inventarnummer, Stempel) und systemseitig in aDIS/BMS (Exemplardatensatz anlegen, Signatur vergeben, Standort zuweisen). Nach erfolgter Inventarisierung wird das Medium im OPAC als vorbestellbar freigeschaltet. |
| O3 | FaMIs | **Rechnung bezahlen** | Die FaMIs prüfen die Lieferantenrechnung auf Richtigkeit (Preise, Mengen, Konditionen) und veranlassen die Bezahlung über das Rechnungssystem SAP in Verbindung mit aDIS/BMS. Die Buchung erfolgt gegen die entsprechende Etatstelle. Die 41-3 Hauptverwaltung wird bei Bedarf einbezogen. |
| O4 | FaMIs | **Erwerbungsdatensatz auffüllen (Katalogisierung)** | Die FaMIs vervollständigen den Erwerbungsdatensatz durch eine vollständige Titelaufnahme in aDIS/BMS: Formalerschließung (Haupt- und Nebeneintragungen, Urheberangaben, Verlagsangaben) sowie Sacherschließung (Schlagwortvergabe, Systematik-Notation, Themengruppen-Zuordnung). Bibliografische Fremddaten aus Fachdatenbanken werden genutzt und nach internen Standards angepasst. |
| O5 | FaMIs | **Medium technisch einarbeiten** | Die FaMIs bereiten das Medium physisch für die Ausleihe vor: Anbringen von Signaturaufklebern, Schutzfolie, Bibliotheksstempel sowie — je nach Medientyp — RFID-Chips oder Sicherungsetiketten. Medientypspezifische Einarbeitungsstandards der Stadtbibliothek Stuttgart werden angewendet (vgl. KATA-Dokumente). |
| O6 | FaMIs | **Medium freibuchen** | Die FaMIs schalten das Medium in aDIS/BMS für die Ausleihe frei (Freibuchung). Das System prüft automatisch, ob eine Vorbestellung vorliegt, und stellt das Medium in diesem Fall unmittelbar für die Abholung bereit. Der Bürger erhält eine Bereitstellungsbenachrichtigung. |

## Key Performance Indicators (KPIs)

### 1. Prozess-KPIs (Ebene Gesamtprozess)

| KPI-ID | Kennzahl | Beschreibung | Zielwert | Messmethode |
| :--- | :--- | :--- | :--- | :--- |
| **P-KPI-01** | **Einarbeitungszeit (Durchlaufzeit)** | Gesamtdauer vom Liefereingang bis zur Freischaltung des Mediums für die Ausleihe. | < 5 Werktage | Timestamp(Freibuchung) – Timestamp(Liefereingang) |
| **P-KPI-02** | **Katalogisierungsqualitätsrate** | Anteil der Katalogisate, die ohne Nachkorrekturen die internen Qualitätsprüfungen bestehen. | > 97 % | Anzahl(fehlerfreie Katalogisate) / Gesamtanzahl(Katalogisate) |
| **P-KPI-03** | **Reklamationsquote** | Anteil der Lieferungen mit Mängeln (fehlerhafte, beschädigte oder fehlende Medien) gemessen an allen Lieferungen. | < 3 % | Anzahl(reklamierte Lieferungen) / Gesamtanzahl(Lieferungen) |
| **P-KPI-04** | **Vorbestellungs-Bereitstellungszeit** | Zeitdauer von der Freibuchung bis zur vollständigen Bereitstellung eines vorgemerkten Mediums für den Kunden. | < 24 Stunden | Timestamp(Bereitstellungsbenachrichtigung) – Timestamp(Freibuchung) |

### 2. Aktivitäts-KPIs (Ebene Prozessschritte)

| Zugeordnete Aktivität(en) | KPI-Name | Beschreibung & Relevanz | Zielwert |
| :--- | :--- | :--- | :--- |
| **O1 Lieferkontrolle** | **Lieferkontrolldauer** | Durchschnittliche Zeit für die vollständige Lieferkontrolle je Lieferung. Relevanz: Engpasspotenzial bei Großlieferungen. | < 2 Stunden/Lieferung |
| **O1 Lieferkontrolle** → **O2 Inventarisieren** | **Zeit bis Vorbestellbarkeit** | Zeitdauer von der Lieferkontrolle bis zur OPAC-Freischaltung als „vorbestellbar". Relevanz: Kundenservice-Qualität. | < 1 Werktag |
| **O3 Rechnung bezahlen** | **Rechnungsbearbeitungsdauer** | Durchschnittliche Bearbeitungszeit je Rechnung von Eingang bis Buchungsbestätigung. Relevanz: Konformität mit Zahlungszielen. | < 10 Werktage |
| **O4 Katalogisierung** | **Katalogisierungszeit je Titel** | Durchschnittliche Bearbeitungszeit für Formal- und Sacherschließung je Titel ohne Fremddaten-Unterstützung. | < 20 Minuten/Titel |
| **O4 Katalogisierung (mit Fremddaten)** | **Fremddaten-Zeitersparnis** | Durchschnittliche Zeitersparnis je Katalogisierung durch Nutzung automatisch übernommener Fremddaten. | > 50 % Zeitersparnis |
| **O5 Technische Einarbeitung** → **O6 Freibuchen** | **Technische Einarbeitungszeit** | Durchschnittliche Bearbeitungszeit für die physische Einarbeitung je Medieneinheit (Signatur, Folie, RFID). | < 5 Minuten/Medium |

## Eingesetzte IT-Systeme
- **aDIS/BMS – Modul Katalogisierung (aStec):** Titelaufnahme, Formal- und Sacherschließung, Exemplardatensatzverwaltung, Freibuchung.
- **aDIS/BMS – Modul Erwerbung (aStec):** Lieferkontrolle gegen Bestelldatensatz, Rechnungskontrolle.
- **aDIS/WebOPAC:** Freischaltung des Mediums für Vorbestellungen nach Inventarisierung; automatische Bereitstellungsbenachrichtigung nach Freibuchung.
- **SAP:** Rechnungsbegleichung und Etatbuchung in Verbindung mit aDIS/BMS.
- **Fachdatenbanken (extern):** Bibliografische Normdaten für die Katalogisierungsunterstützung.

## Referenzdokumente
- BPMN-Modell: `CreateBPMN/Bibliothek_Medienbestand_TP4_Medien_einarbeiten.bpmn`
- Katalogisierungsrichtlinien Stadtbibliothek Stuttgart (KATA-Dokumente): `KATA_hörbuch.pdf`, `KATA_mehrbändigeWerke.pdf`, `KATA_Reihen.pdf` u.a.
- Steckbrief TP3: `CreateSteckbrief/Prozesssteckbrief_Bibliothek_TP3_Medien_erwerben.md`
