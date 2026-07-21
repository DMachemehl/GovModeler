# Prozesssteckbrief: TP3 Medien erwerben

## Zusammenfassung
Der Prozess **„TP3 Medien erwerben"** bildet die operative Beschaffungsphase innerhalb des übergeordneten Prozesses „Medienbestand managen" der Stadtbibliothek Stuttgart. Er beginnt mit dem Eingang der Kaufentscheidung aus TP2 und führt über die Anlage von Erwerbungsdatensätzen in aDIS/BMS, die Übernahme bibliografischer Fremddaten, die Lieferantenauswahl und die Bestellabgabe zur systemseitigen Verarbeitung durch das IT-Fachverfahren aDIS. Der Prozess endet mit der Freischaltung der bestellten Medien im OPAC, sodass Bürgerinnen und Bürger den Bestellstatus einsehen und Vorbestellungen aufgeben können. Ziel ist eine fehlerfreie, effiziente und für Nutzer:innen transparente Medienbestellung.

## Stammdaten
| Attribut | Wert |
| :--- | :--- |
| **Prozessname** | TP3 Medien erwerben |
| **Übergeordneter Prozess** | Medienbestand managen – Stadtbibliothek Stuttgart |
| **Prozesskategorie** | Bibliotheksmanagement / Medienbestandsmanagement |
| **Auslöser** | Kaufentscheidung und Medienwunsch eingegangen |
| **Ergebnis** | Medium ist bestellt und Bestellung ist im OPAC sichtbar |
| **Hauptverantwortung** | FaMIs (Fachangestellte für Medien- und Informationsdienste) |
| **Beteiligte Rollen** | FaMIs, IT (aDIS) Fachverfahren, Bibliotheksnutzer (Kunde) |
| **Supplier** | Lektoratsteam (Kaufentscheidung aus TP2), Fremddatenanbieter (bibliografische Normdaten) |
| **Vorgelagerter Prozess** | TP2 Markt sichten |
| **Nachgelagerter Prozess** | TP4 Medien einarbeiten |
| **BPMN-Modell** | Bibliothek_Medienbestand_TP3_Medien_erwerben.bpmn |

## Prozessziele
1. **Effizienz:** Minimierung der Durchlaufzeit von der Kaufentscheidung bis zur abgeschickten Bestellung durch strukturierte Erfassungs- und Bestellprozesse.
2. **Datenqualität:** Sicherstellung vollständiger und normierter Erwerbungsdatensätze durch automatisierte Fremddatenübernahme.
3. **Transparenz:** Unmittelbare Sichtbarkeit bestellter Medien im öffentlichen OPAC zur Information der Bibliotheksnutzer:innen.
4. **Serviceorientierung:** Ermöglichung von Vorbestellungen auf noch nicht eingetroffene Medien direkt nach der Bestellabgabe.
5. **Revisionssicherheit:** Lückenlose Dokumentation aller Bestellvorgänge in aDIS/BMS für Rechnungskontrolle und Bestandssteuerung.

## Detaillierte Prozessschritte

### Pool: Kunde (Bibliotheksnutzer / Bürger)

| Nr. | Schritt | Beschreibung |
| :--- | :--- | :--- |
| K1 | **Medienwunsch und Vorbestellung aufgeben** | Der Bürger gibt einen konkreten Medienwunsch oder Anschaffungsvorschlag ab — persönlich am Auskunftsdienst, über den OPAC (aDIS/WebOPAC) oder digitale Kanäle. Dieser Wunsch fließt als Bedarfssignal in den Erwerbungsprozess ein. |
| K2 | **Bestellstatus im OPAC einsehen** | Sobald die Bestellung im aDIS/BMS-System verarbeitet und im OPAC freigeschaltet ist, kann der Bürger den Bestellstatus einsehen und das Medium für die spätere Einarbeitung vormerken. |

### Pool: Organisation

| Nr. | Rolle/Lane | Schritt | Beschreibung |
| :--- | :--- | :--- | :--- |
| O1 | FaMIs | **Erwerbungsdatensatz anlegen** | Die FaMIs legen für jeden zu bestellenden Titel einen Erwerbungsdatensatz im Erwerbungsmodul von aDIS/BMS an. Der Datensatz enthält alle kaufmäßig relevanten Informationen: Titel, ISBN, Verlag, Erscheinungsjahr, Exemplaranzahl, Standort, Etatstelle sowie interne Klassifizierungen gemäß der Kaufempfehlung des Lektoratsteams. |
| O2 | IT (aDIS) | **Fremddaten in aDIS übernehmen** | Das aDIS/BMS-System übernimmt automatisiert bibliografische Fremddaten von externen Fremddatenanbietern (z.B. Deutsche Bibliothek, Verbundkataloge). Die Fremddaten werden mit den angelegten Erwerbungsdatensätzen verknüpft und ermöglichen eine qualitätsgesicherte, normierte Titelerfassung ohne manuelle Doppelerfassung. |
| O3 | FaMIs | **Lieferant auswählen** | Die FaMIs wählen den geeigneten Lieferanten für die jeweilige Bestellung aus. Die Auswahl berücksichtigt Lieferbedingungen, Konditionen und Verfügbarkeit. Der ausgewählte Lieferant wird dem Erwerbungsdatensatz in aDIS/BMS zugeordnet. |
| O4 | FaMIs | **Bestellung sammeln und abschicken** | Die FaMIs sammeln alle bearbeiteten Erwerbungsdatensätze zur Sammelbestellung und schicken diese über das Erwerbungsmodul von aDIS/BMS an den ausgewählten Lieferanten ab. |
| O5 | IT (aDIS) | **Bestelldaten in aDIS verarbeiten** | Das aDIS/BMS-System verarbeitet die abgeschickten Bestelldaten: Es erstellt Bestellbelege, bucht die bestellten Titel gegen die jeweiligen Etats und bereitet die Bestellvorgänge für die Lieferkontrolle in TP4 vor. Der Bestellvorgang ist systemseitig dokumentiert und revisionssicher gespeichert. |
| O6 | IT (aDIS) | **Bestellung im OPAC bereitstellen** | Das aDIS/BMS-System schaltet die bestellten Titel im öffentlichen OPAC (aDIS/WebOPAC) für Bibliotheksnutzer:innen sichtbar. Bürgerinnen und Bürger können den Bestellstatus einsehen und das Medium bereits vor Lieferung vormerken. |

## Key Performance Indicators (KPIs)

### 1. Prozess-KPIs (Ebene Gesamtprozess)

| KPI-ID | Kennzahl | Beschreibung | Zielwert | Messmethode |
| :--- | :--- | :--- | :--- | :--- |
| **P-KPI-01** | **Time-to-Order (Durchlaufzeit)** | Gesamtdauer von der eingegangenen Kaufentscheidung bis zur abgeschickten Bestellung an den Lieferanten. | < 5 Werktage | Timestamp(Bestellabgang) – Timestamp(Kaufentscheidung eingegangen) |
| **P-KPI-02** | **OPAC-Sichtbarkeitszeit** | Zeitdauer zwischen Bestellabgang und Freischaltung der bestellten Titel im öffentlichen OPAC. | < 24 Stunden | Timestamp(OPAC-Freischaltung) – Timestamp(Bestellabgang) |
| **P-KPI-03** | **Bestellfehlerquote** | Anteil der Bestellvorgänge, die aufgrund fehlerhafter oder unvollständiger Datensätze korrigiert werden müssen. | < 2 % | Anzahl(korrigierte Bestellungen) / Gesamtanzahl(Bestellvorgänge) |
| **P-KPI-04** | **Fremddaten-Übernahmequote** | Anteil der Erwerbungsdatensätze, bei denen bibliografische Fremddaten automatisiert übernommen werden konnten. | > 85 % | Anzahl(Datensätze mit Fremddaten) / Gesamtanzahl(Datensätze) |

### 2. Aktivitäts-KPIs (Ebene Prozessschritte)

| Zugeordnete Aktivität(en) | KPI-Name | Beschreibung & Relevanz | Zielwert |
| :--- | :--- | :--- | :--- |
| **O1 Erwerbungsdatensatz anlegen** (FaMIs) | **Datensatz-Anlagezeit** | Durchschnittliche Zeit je Erwerbungsdatensatz vom Beginn der Erfassung bis zur Vollständigkeit. Relevanz: Effizienz im manuellen Kernschritt. | < 5 Minuten/Datensatz |
| **O1 Datensatz anlegen** → **O2 Fremddaten übernehmen** (IT) | **Fremddaten-Matching-Rate** | Anteil der Datensätze, bei denen automatisch passende Fremddaten gefunden und verknüpft werden. Relevanz: Datenqualität und Zeitersparnis. | > 85 % |
| **O2 Fremddaten** → **O3 Lieferant auswählen** (FaMIs) | **Lieferantenentscheidungszeit** | Durchschnittliche Zeit für die Lieferantenauswahl je Bestellposition. Relevanz: Engpasspotenzial bei Speziallieferungen. | < 2 Minuten/Position |
| **O4 Bestellung abschicken** → **O5 Bestelldaten verarbeiten** (IT) | **Systemverarbeitungszeit** | Zeit zwischen Bestellabgang durch FaMIs und vollständiger systemseitiger Verarbeitung in aDIS. Relevanz: Technische Performance. | < 30 Minuten |
| **O5 Bestelldaten verarbeiten** → **O6 OPAC bereitstellen** (IT) | **OPAC-Freischaltungsdauer** | Zeit von der abgeschlossenen Systemverarbeitung bis zur Sichtbarkeit im öffentlichen OPAC. Relevanz: Kundenwahrnehmung und Vorbestellmöglichkeit. | < 1 Stunde |
| **O6 OPAC bereitstellen** → **K2 Bestellstatus einsehen** | **Vorbestellungskonversionsrate** | Anteil der im OPAC sichtbaren Bestellungen, die von Nutzer:innen aktiv vorgemerkt werden. Relevanz: Messung der Bedarfskongruenz. | > 15 % |

## Eingesetzte IT-Systeme
- **aDIS/BMS – Modul Erwerbung (aStec):** Kernmodul für Erwerbungsdatensatzanlage, Lieferantenauswahl, Bestellabgang und revisionssichere Dokumentation.
- **aDIS/WebOPAC:** Öffentlicher Online-Katalog; stellt bestellte Medien für Nutzer:innen sichtbar und ermöglicht Vorbestellungen.
- **Fremddatenanbieter (externe Systeme):** Bibliografische Normdaten von Deutschen Bibliotheksverbünden (z.B. hbz, BVB) zur automatisierten Datensatzanreicherung.

## Referenzdokumente
- BPMN-Modell: `CreateBPMN/Bibliothek_Medienbestand_TP3_Medien_erwerben.bpmn`
- Steckbrief TP2: `CreateSteckbrief/Prozesssteckbrief_Bibliothek_TP2_Markt_sichten.md`
