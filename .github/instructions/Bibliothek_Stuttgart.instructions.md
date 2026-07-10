---
applyTo: '**/*Bibliothek*.bpmn'
description: 'Fachterminologie und Prozessrichtlinien fuer Bibliotheksprozesse der Stadtbibliothek Stuttgart. Use when: modeling library processes, creating BPMN for Stuttgart public library, working with Bibliothek files.'
---

# Bibliotheksprozesse Stadtbibliothek Stuttgart

## Quelldokumente der Stadtbibliothek Stuttgart

Im Ordner `Prozessbeschreibungen - Anleitungen/` sind offizielle Dokumente der Stadtbibliothek Stuttgart hinterlegt. Diese MUESSEN bei der Modellierung der jeweiligen Prozesse als primaere Informationsquelle herangezogen werden.

| Datei | Thema |
|-------|-------|
| `bücher.pdf` | Prozesse rund um Buecher |
| `ProzessBlockbestaende.pdf` | Prozess Blockbestaende |
| `ProzessRotationsbestaende.pdf` | Prozess Rotationsbestaende |
| `Blockbestand_ZB_STBs.pdf` | Blockbestand Zentralbibliothek und Stadtteilbibliotheken |
| `Medienpakete.pdf` | Umgang mit Medienpaketen |
| `Letztexemplare.xlsx` | Verwaltung von Letztexemplaren |
| `Verlage_Neuaufnahme.pdf` | Neuaufnahme von Verlagen |
| `KATA_hörbuch.pdf` | Katalogisierung Hoerbuecher |
| `KATA_mehrbändigeWerke.pdf` | Katalogisierung mehrbaendige Werke |
| `KATA_E-Journals.pdf` | Katalogisierung E-Journals |
| `KATA_Reihen.pdf` | Katalogisierung Reihen |
| `KATA_Erinnerungskoffer.pdf` | Katalogisierung Erinnerungskoffer |
| `KATA_Podcasts.pdf` | Katalogisierung Podcasts |
| `KATA_FremdsprachigeMedien_Titel.pdf` | Katalogisierung fremdsprachige Medien |
| `KATA_Tonies.pdf` | Katalogisierung Tonies |
| `KATA_Konsolenspiele.pdf` | Katalogisierung Konsolenspiele |
| `KATA_enthalteneWerke.pdf` | Katalogisierung enthaltene Werke |
| `KATA_Kamishibai_und_andere_Karten.pdf` | Katalogisierung Kamishibai und Karten |
| `Bestandsprofile_Literatur_ausführlich.xlsx` | Bestandsprofile Literatur |
| `Bestandsprofil Kibi 2022.docx` | Bestandsprofil Kinderbibliothek |

**Hinweis**: Vor der Modellierung eines Prozesses pruefen, ob ein passendes Dokument in diesem Ordner vorliegt, und dieses lesen, um prozessspezifische Details korrekt abzubilden.

## Organisationsstruktur

### Abteilungen/Organisationseinheiten
- **Ausleihe**: Medienausleihe, Rueckgabe, Verlaengerungen; verantwortlich fuer alle physischen Medien und Dinge zum Ausleihen
- **Auskunft/Information**: Beratung, Rechercheanfragen, Datenbankzugriff, Themenwelten (kuratierte Medienlisten)
- **Erwerbung**: Medienanschaffung, Bestellwesen, Lieferantenmanagement
- **Katalogisierung**: Medienerschliessung, Titelaufnahme, Sacherschliessung
- **Fernleihe**: Leihverkehr zwischen Bibliotheken
- **Veranstaltungen**: Lesungen, Fuehrungen, Workshops, Kinder- und Jugendbuchwochen, Escape-Games
- **Digitale Dienste**: eBibliothek, Onleihe 3, filmfriend, E-Medien, Datenbanken
- **Kinderbibliothek (KiBi)**: Spezialabteilung fuer Kinder; eigene Zweigstelle mit separatem Bestandsprofil

### IT-Systeme (Black-Box)
- **aDIS/BMS** (aStec): Zentrales Bibliotheksmanagementsystem der Stadtbibliothek Stuttgart; entwickelt von der Firma aStec (astec eG), barrierefreie Software, seit Jahrzehnten im Bibliothekswesen eingesetzt
  - Modul **Ausleihe/Benutzung**: Ausleihe, Rueckgabe, Verlaengerung, Benutzerverwaltung, Mahnwesen, Gebuehren
  - Modul **Katalogisierung**: Titelaufnahme, Sacherschliessung, Medienerschliessung
  - Modul **Erwerbung**: Bestellwesen, Lieferantenmanagement, Medienanschaffung
  - Modul **Fernleihe**: Leihverkehr zwischen Bibliotheken
  - Modul **OPAC (aDIS/WebOPAC)**: Online-Katalog fuer Nutzerrecherche und Selbstbedienungsfunktionen (Kontoansicht unter "Mein Konto", Verlaengerung, Vormerkung); mit integriertem KI-Chatbot
- **Onleihe 3**: Digitale Ausleihe von E-Books, E-Audios, E-Papers (Plattform wurde 2026 auf Version 3 umgestellt)
- **filmfriend**: Streaming-Plattform fuer Filme und Serien (stuttgart.filmfriend.de)
- **Kassensystem**: Gebuehrenverwaltung und Barzahlungsabwicklung

## Fachterminologie

### Benutzer/Kunden
| Begriff | Beschreibung |
|---------|--------------|
| Bibliotheksnutzer | Person mit gueltigem Leserausweis |
| Leserausweis | Berechtigungsnachweis zur Bibliotheksnutzung |
| Benutzerkonto | Elektronisches Konto im BMS |
| Anmeldung | Erstregistrierung als Bibliotheksnutzer |
| Verlaengerung | Erneuerung des Leserausweises |

### Medien und Ausleihe
| Begriff | Beschreibung |
|---------|--------------|
| Medium | Buch, Zeitschrift, DVD, CD, E-Book etc. |
| Signatur | Standortkennung des Mediums |
| Exemplar | Physisches Stueck eines Titels |
| Ausleihe | Zeitlich begrenzte Medienuebergabe |
| Rueckgabe | Rueckfuehrung entliehener Medien |
| Verlaengerung | Fristverlaengerung der Ausleihe |
| Vormerkung | Reservierung entliehener Medien |
| Leihfrist | Zeitraum der erlaubten Ausleihe |

### Fernleihe
| Begriff | Beschreibung |
|---------|--------------|
| Gebende Bibliothek | Bibliothek, die Medium versendet |
| Nehmende Bibliothek | Bibliothek, die Medium bestellt |
| Leihverkehrsordnung | Regelwerk fuer Fernleihe |
| Bestellschein | Fernleihbestellformular |

### Gebuehren und Mahnwesen
| Begriff | Beschreibung |
|---------|--------------|
| Jahresgebuehr | Jaehrlicher Mitgliedsbeitrag |
| Saeumnisgebuehr | Gebuehr bei Fristueberziehung |
| Mahnung | Erinnerung an ueberfaellige Medien |
| Mahnstufe | Eskalationsstufe im Mahnwesen |
| Ersatzleistung | Kosten bei Medienverlust |

## Prozessmuster

### Standardablauf Medienausleihe
1. Ausleihwunsch eingegangen (Kunde → Organisation)
2. Benutzerkonto in aDIS/BMS pruefen (Organisation → IT)
3. Kontostatus erhalten (IT → Organisation)
4. Verfuegbarkeit in aDIS/BMS pruefen (Organisation → IT)
5. Verfuegbarkeitsstatus erhalten (IT → Organisation)
6. Medium bereitstellen
7. Ausleihe in aDIS/BMS buchen (Organisation → IT)
8. Buchungsbestaetigung erhalten (IT → Organisation)
9. Medium aushaendigen (Organisation → Kunde)

### Standardablauf Leserausweis beantragen
1. Antrag eingegangen (Kunde → Organisation)
2. Personalien erfassen
3. Identitaet pruefen
4. Benutzerkonto in aDIS/BMS anlegen (Organisation → IT)
5. Kontobestaetigung erhalten (IT → Organisation)
6. Leserausweis ausstellen
7. Ausweis aushaendigen (Organisation → Kunde)

### Standardablauf Vormerkung
1. Vormerkungswunsch eingegangen (Kunde → Organisation)
2. Benutzerkonto in aDIS/BMS pruefen (Organisation → IT)
3. Kontostatus erhalten (IT → Organisation)
4. Vormerkung in aDIS/BMS erfassen (Organisation → IT)
5. Vormerkungsbestaetigung erhalten (IT → Organisation)
6. Bestaetigung senden (Organisation → Kunde)
7. [Bei Rueckgabe] Bereitstellungsbenachrichtigung versenden (Organisation → Kunde)

### Standardablauf Fernleihe (nehmend)
1. Fernleihanfrage eingegangen (Kunde → Organisation)
2. Lokalen Bestand pruefen
3. Fernleihbestellung aufgeben
4. Medium empfangen
5. Bereitstellungsbenachrichtigung senden (Organisation → Kunde)
6. Medium aushändigen (Organisation → Kunde)

## Message Flows (Black-Box Pools)

### Kunde → Organisation
- Ausleihwunsch
- Rueckgabemeldung
- Verlaengerungsantrag
- Vormerkungswunsch
- Leserausweis-Antrag
- Rechercheanfrage
- Fernleihanfrage
- Veranstaltungsanmeldung
- Anschaffungsvorschlag

### Organisation → Kunde
- Abholbenachrichtigung
- Verlaengerungsbestaetigung
- Mahnung
- Leserausweis
- Rechercheauskunft
- Bereitstellungsbenachrichtigung
- Veranstaltungsbestaetigung

### Organisation → IT (aDIS/BMS)
- Kontoabfrage
- Verfuegbarkeitspruefung
- Ausleihbuchung
- Rueckgabebuchung
- Verlaengerungsbuchung
- Vormerkungserfassung
- Kontoanlage
- Mahnlaufanstoss
- Erwerbungsbestellung
- Katalogisierungsauftrag

### IT (aDIS/BMS) → Organisation
- Kontostatus
- Verfuegbarkeitsstatus
- Buchungsbestaetigung
- Vormerkungsbestaetigung
- Kontoerstellungsbestaetigung
- Mahnliste
- Bestellbestaetigung
- Katalogdaten

## Benennungskonventionen

### Task-Namen (Substantiv + Verb)
- Benutzerkonto pruefen
- Verfuegbarkeit pruefen
- Medium bereitstellen
- Ausleihe buchen
- Vormerkung erfassen
- Leserausweis ausstellen
- Mahnung versenden
- Gebuehr berechnen

### Event-Namen (Perfekt/Zustand)
- **Start**: Ausleihwunsch eingegangen, Antrag eingereicht, Rueckgabe erfolgt
- **End**: Medium ausgeliehen, Leserausweis ausgestellt, Vormerkung eingetragen

### Dateinamen
- Praefix: `Bibliothek_`
- Prozessname: Substantiv_Verb
- Beispiele:
  - `Bibliothek_Medienausleihe.bpmn`
  - `Bibliothek_Leserausweis_beantragen.bpmn`
  - `Bibliothek_Fernleihe_bestellen.bpmn`
  - `Bibliothek_Vormerkung_einloesen.bpmn`

## Besonderheiten Stadtbibliothek Stuttgart

### Standorte
Die Stadtbibliothek Stuttgart besteht aus:
- **Zentralbibliothek am Mailaender Platz** (Adresse: Mailaender Platz 1, 70173 Stuttgart) — Hauptstandort
- **18 Stadtteilbibliotheken** — darunter Weilimdorf, Feuerbach, Botnang, Kneippweg u.a.
- **2 Pop-Up-Bibliotheken** — temporaere Angebote
- **Fahrbibliothek** — mobiler Dienst fuer Stadtteile ohne stationaere Bibliothek
- **eBibliothek** — vollstaendig digitales Angebot (Onleihe 3, filmfriend etc.)

### Selbstverstaendnis
- Aufenthaltsort und Treffpunkt fuer alle
- Lese- und Lernplaetze
- Vielfaeltiges Veranstaltungsprogramm
- Grosse Auswahl an Medien **und Dingen** zum Ausleihen (nicht nur Medien)

### Spezielle Angebote
- **Kinderbibliothek (KiBi)**: Spezialbibliothek fuer Kinder mit eigenem Bestandsprofil; Zweigstelle am Kneippweg
- **Kinder- und Jugendbuchwochen**: Jaehrliches Literaturfestival (Lesungen, Workshops, Ausstellungen)
- **Themenwelten**: Kuratierte Medienlisten zu bestimmten Themen
- **Escape-Game "Die Schluesselbucher"**: Familienfreundliches Abenteuer in den Stadtteilbibliotheken Weilimdorf, Feuerbach und Botnang
- **Wikipedia-Editierworkshops**: Regelmaessige Veranstaltungen in der Zentralbibliothek

### Digitale Angebote
- **Onleihe 3**: E-Books, E-Audios, E-Papers (2026 auf Version 3 umgestellt)
- **filmfriend**: Streaming von Filmen und Serien (stuttgart.filmfriend.de)
- **aDIS/WebOPAC mit KI-Chatbot**: Integrierter KI-Assistent fuer die Katalogsuche (in Kooperation mit aStec und reelport)
- Pressreader
- Munzinger-Datenbanken

### Rechtliche Grundlagen
- Benutzungs- und Gebuehrenverordnung: https://stadtbibliothek-stuttgart.de/content/info/gebuehren.html
