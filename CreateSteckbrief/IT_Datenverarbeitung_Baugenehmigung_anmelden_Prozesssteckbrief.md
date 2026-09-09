# Prozesssteckbrief: Baugenehmigung anmelden

## Zusammenfassung

Der Prozess **„Baugenehmigung anmelden"** beschreibt die vollautomatisierte, systemübergreifende Datenverarbeitung eines digital eingereichten Bauantrags. Ausgehend vom Eingang der Antragsdaten im Bauantrags-Portal durchläuft der Prozess drei weitere IT-Subsysteme – Fachverfahren Bauaufsicht, Liegenschaftskataster/GIS-System und Dokumenten-Management-System (DMS) –, die als eigenständige Pools in einer BPMN-Kollaboration modelliert sind. Ziel ist die konsistente, rechtssichere und medienbruchfreie Bearbeitung des Bauantrags von der Antragseinreichung bis zur archivierten und bereitgestellten Baugenehmigung, ohne manuelle Sachbearbeitung im Standardpfad (Happy Path).

---

## Stammdaten

| Attribut | Wert |
| :--- | :--- |
| **Prozessname** | Baugenehmigung anmelden |
| **Prozesskategorie** | IT-Datenverarbeitung / Bauaufsicht & Bauordnungsrecht |
| **Auslöser** | Bauantrag über Online-Portal eingegangen (HTTPS POST, XBau-konforme Nachricht) |
| **Ergebnis** | Baugenehmigung archiviert und bereitgestellt |
| **Prozesstyp** | Vollautomatisierter IT-Hintergrundprozess (keine manuelle Sachbearbeitung im Standardpfad) |
| **Hauptverantwortung** | Untere Bauaufsichtsbehörde / Fachbereich Bauordnung |
| **Beteiligte IT-Systeme (Pools)** | Bauantrags-Portal, Fachverfahren Bauaufsicht, Liegenschaftskataster/GIS-System, Dokumenten-Management-System (DMS) |
| **Aufgerufene Standards/Subsysteme** | XBau (XÖV-Standard Bauantragsdaten), ALKIS (Amtliches Liegenschaftskatasterinformationssystem) |
| **BPMN-Modell** | `IT_Datenverarbeitung_Baugenehmigung_anmelden.bpmn` |
| **Erstellt am** | 09.09.2026 |
| **Version** | 1.0 |

---

## Prozessziele

1. **Automatisierung:** Vollständige Eliminierung manueller Sachbearbeitungsschritte im Standardpfad durch End-to-End-Orchestrierung von Portal, Fachverfahren, Kataster und DMS.
2. **Rechtssicherheit:** Sicherstellung einer bebauungsplankonformen Prüfung sowie korrekter Gebührenberechnung auf Basis valider Flurstücksdaten aus dem Liegenschaftskataster.
3. **Datenintegrität:** Konsistente, vollständige Datensätze in Fachverfahren und DMS durch strukturierte Validierung und transaktionale Verarbeitung in jedem Prozessschritt.
4. **Nachvollziehbarkeit:** Revisionssichere, medienbruchfreie Archivierung des Baugenehmigungsbescheids inklusive aller Metadaten im DMS.
5. **Interoperabilität:** Nutzung standardisierter Austauschformate (XBau, ALKIS) zur reibungslosen Kommunikation zwischen den beteiligten Fachsystemen.

---

## Technische Rahmenbedingungen

### Plattform & Infrastruktur

| Parameter | Wert |
| :--- | :--- |
| **Plattform** | Kommunale Fachverfahrenslandschaft (Bauaufsicht), OZG-konformes Online-Portal |
| **Ausführungsumgebung** | Landes-/Kommunales Rechenzentrum (On-Premise oder Government-Cloud) |
| **API-Protokoll** | REST / JSON und XML (XBau) über HTTPS (TLS 1.2+) |
| **Interne Kommunikation** | Asynchrones Messaging (Message Queue) zwischen Fachverfahren, GIS und DMS |
| **Authentifizierung** | OAuth 2.0 (Bearer Token) bzw. Servicekonto-Zertifikate (Mutual TLS) für System-zu-System-Kommunikation |
| **Autorisierung** | Rollen-/Rechtekonzept je Fachverfahren (z. B. Sachbearbeitung Bauaufsicht, Katasteramt, Registratur) |
| **Datenaustauschstandard** | XBau (XÖV-Standard für Bauantragsdaten) |
| **Geodatenstandard** | ALKIS (Amtliches Liegenschaftskatasterinformationssystem) |
| **Dokumentenformat** | PDF/A (Bescheid, revisionssicher), JSON/XML (Metadaten) |

### API-Endpunkt (Einstiegspunkt Bauantrags-Portal)

| Parameter | Wert |
| :--- | :--- |
| **Methode** | `POST` |
| **Endpunkt** | `/api/bauantrag/v1/antraege` |
| **Content-Type** | `application/json` |
| **Accept** | `application/json` |

**Beispiel-Request-Payload:**
```json
{
  "antrags_id": "BA-2026-004532",
  "bauherr": {
    "name": "Max Mustermann",
    "anschrift": "Musterstraße 12, 70173 Stuttgart"
  },
  "flurstueck_nr": "1234/5",
  "gemarkung": "Stuttgart-Mitte",
  "bauvorhaben_typ": "Neubau Einfamilienhaus",
  "anlagen": [
    { "typ": "Lageplan", "format": "application/pdf", "groesse_kb": 2048 },
    { "typ": "Baubeschreibung", "format": "application/pdf", "groesse_kb": 512 },
    { "typ": "Statiknachweis", "format": "application/pdf", "groesse_kb": 1024 }
  ]
}
```

**Pflichtfelder:**
- `antrags_id` (String, systemgeneriert, eindeutig)
- `flurstueck_nr` (String, Referenz auf ALKIS-Flurstück)
- `bauvorhaben_typ` (Choice: `Neubau`, `Anbau`, `Umbau`, `Nutzungsänderung`)
- `anlagen[]` (mind. Lageplan und Baubeschreibung als PDF)

---

## Prozessablauf (End-to-End)

### Pool 1 – Bauantrags-Portal

| Schritt | Aktivität | Typ | Input | Output |
| :---: | :--- | :--- | :--- | :--- |
| 1 | Antragsdaten empfangen | Service Task | HTTPS POST JSON-Payload | Rohdatensatz im internen Format |
| 2 | Datenformat validieren | Service Task | Rohdatensatz | Validiertes Objekt oder Fehlerantwort (HTTP 400) |
| 3 | Vollständigkeit prüfen | Service Task | Validiertes Objekt | Vollständigkeitsstatus (Pflichtfelder, Anlagen) |
| 4 | Antragsunterlagen zwischenspeichern | Service Task | Antragsdaten + Anlagen | Persistierter Zwischenspeicher-Datensatz |
| 5 | Antragsdaten an Fachverfahren übermitteln | Send Task | Vollständiger Antragsdatensatz | XBau-Nachricht `Bauantragsdaten` an Fachverfahren |

**Fehlerbehandlung Pool 1:**
- Formatfehler → HTTP 400 mit strukturiertem Error-Body
- Fehlende Pflichtanlagen (z. B. kein Lageplan) → HTTP 422, Antrag verbleibt im Status `unvollständig`

---

### Pool 2 – Fachverfahren Bauaufsicht

| Schritt | Aktivität | Typ | Input | Output |
| :---: | :--- | :--- | :--- | :--- |
| 6 | Antragsdaten auf Plausibilität validieren | Service Task | XBau-Nachricht `Bauantragsdaten` | Plausibilisierter Antragsdatensatz |
| 7 | Flurstücksdaten anfordern | Send Task | Flurstücksnummer, Gemarkung | ALKIS-Anfrage an GIS-System |
| 8 | Flurstücksdaten übernehmen | Service Task | ALKIS-Antwortdaten | Angereicherter Antragsdatensatz (Flurstücksgeometrie, Nutzungsart) |
| 9 | Bebauungsplan-Konformität prüfen | Service Task | Angereicherter Antragsdatensatz | Konformitätsstatus (konform/nicht konform) |
| 10 | Baugebühr berechnen | Service Task | Bauvorhaben-Typ, Bruttogrundfläche | Gebührenbescheid-Datensatz |
| 11 | Baugenehmigungsbescheid generieren | Service Task | Konformitätsstatus, Gebührendatensatz | Baugenehmigungsbescheid (PDF/A) |
| 12 | Bescheid an DMS übermitteln | Send Task | Baugenehmigungsbescheid + Metadaten | Nachricht `Baugenehmigungsbescheid` an DMS |

**Datenbankfelder Fachverfahren (Auszug):**

| Feldname | Typ | Pflicht | Beschreibung |
| :--- | :--- | :---: | :--- |
| `antrags_id` | String | ✓ | Eindeutige Antragskennung |
| `flurstueck_nr` | String | ✓ | Referenz auf ALKIS-Flurstück |
| `bebauungsplan_konform` | Boolean | ✓ | Ergebnis der Konformitätsprüfung |
| `gebuehr_betrag` | Decimal | ✓ | Berechnete Baugebühr in EUR |
| `bescheid_aktenzeichen` | String | ✓ | Systemgeneriertes Aktenzeichen |
| `bescheid_status` | Choice | ✓ | `erstellt`, `versendet`, `archiviert` |

---

### Pool 3 – Liegenschaftskataster / GIS-System

| Schritt | Aktivität | Typ | Input | Output |
| :---: | :--- | :--- | :--- | :--- |
| 13 | Flurstücksanfrage validieren | Service Task | Flurstücksnummer, Gemarkung | Validierte Katasteranfrage |
| 14 | Flurstücksdaten aus Kataster abrufen | Service Task | Validierte Katasteranfrage | ALKIS-Rohdatensatz (Geometrie, Nutzungsart, Eigentümer) |
| 15 | Geodaten aufbereiten | Service Task | ALKIS-Rohdatensatz | Fachverfahren-kompatibler Datensatz |
| 16 | Flurstücksdaten an Fachverfahren übermitteln | Send Task | Aufbereiteter Geodatensatz | Nachricht `Flurstücksdaten` an Fachverfahren |

**ALKIS-Datenfelder (Auszug):**

| Feldname | Typ | Beschreibung |
| :--- | :--- | :--- |
| `flurstueck_nr` | String | Amtliche Flurstücksnummer |
| `gemarkung` | String | Zugehörige Gemarkung |
| `flaeche_qm` | Decimal | Flurstücksfläche in Quadratmetern |
| `nutzungsart` | Choice | Amtliche Nutzungsart (z. B. Wohnbaufläche, Gewerbefläche) |
| `geometrie` | GeoJSON/WKT | Flurstücksgeometrie |

---

### Pool 4 – Dokumenten-Management-System (DMS)

| Schritt | Aktivität | Typ | Input | Output |
| :---: | :--- | :--- | :--- | :--- |
| 17 | Bescheid empfangen | Service Task | Nachricht `Baugenehmigungsbescheid` | Eingegangener Dokumentendatensatz |
| 18 | Metadaten indexieren | Service Task | Aktenzeichen, Flurstücksnummer, Bauherr | Indexierter Metadatensatz |
| 19 | Dokument archivieren | Service Task | PDF/A-Dokument + Metadaten | Revisionssicher archiviertes Dokument |
| 20 | Baugenehmigung bereitstellen | Service Task | Archivierter Dokumentendatensatz | Bereitgestellte Baugenehmigung (Statusaktualisierung im Portal) |

---

## Datenschnittstellen (Message Flows)

| Message | Sender-Pool | Empfänger-Pool | Protokoll | Payload-Typ | Retry-Logik |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `Bauantragsdaten` | Bauantrags-Portal | Fachverfahren Bauaufsicht | HTTPS/REST | XBau (XML/JSON) | 3 Versuche, 30s Intervall |
| `Flurstücksanfrage` | Fachverfahren Bauaufsicht | Liegenschaftskataster/GIS | HTTPS/REST | ALKIS-Anfrage (XML) | 3 Versuche, 30s Intervall |
| `Flurstücksdaten` | Liegenschaftskataster/GIS | Fachverfahren Bauaufsicht | HTTPS/REST | ALKIS-Antwort (GeoJSON) | 3 Versuche, 30s Intervall |
| `Baugenehmigungsbescheid` | Fachverfahren Bauaufsicht | Dokumenten-Management-System | HTTPS/REST | PDF/A + JSON-Metadaten | 3 Versuche, 30s Intervall |

---

## Key Performance Indicators (KPIs)

### 1. Prozess-KPIs (Ebene Gesamtprozess)

| KPI-ID | Kennzahl | Beschreibung | Zielwert | Messmethode |
| :--- | :--- | :--- | :--- | :--- |
| **P-KPI-01** | **End-to-End-Durchlaufzeit** | Gesamtdauer vom Empfang des Bauantrags bis zur Bereitstellung der archivierten Baugenehmigung (automatisierter Standardpfad) | < 5 Minuten | Timestamp(Endereignis DMS) − Timestamp(Startereignis Portal) |
| **P-KPI-02** | **Prozesserfolgsrate** | Anteil erfolgreich abgeschlossener Bauanträge ohne Fehlerfall oder manuelle Korrektur | > 97 % | Anzahl(Status=`archiviert`) / Gesamtanzahl Prozessinstanzen |
| **P-KPI-03** | **Datenqualitätsrate** | Anteil der Anträge, die alle Pflichtfelder und Pflichtanlagen vollständig und valide enthalten | > 95 % | Anzahl(vollständige Anträge) / Gesamtanzahl eingereichter Anträge |
| **P-KPI-04** | **Kataster-Antwortrate** | Anteil der Flurstücksanfragen, die vom GIS-System erfolgreich und fehlerfrei beantwortet werden | > 99 % | Anzahl(erfolgreiche ALKIS-Antworten) / Gesamtanzahl Anfragen |
| **P-KPI-05** | **Archivierungsquote** | Anteil der Baugenehmigungsbescheide, die vollständig indexiert und revisionssicher archiviert werden | 100 % | Anzahl(archivierte Bescheide) / Gesamtanzahl generierter Bescheide |

### 2. Aktivitäts-KPIs (Ebene Prozessschritte)

| Aktivität(en) | KPI-Name | Beschreibung & Relevanz | Zielwert |
| :--- | :--- | :--- | :--- |
| **Antragsdaten empfangen** (Portal) → **Datenformat validieren** (Portal) | **Time-to-Validation** | Dauer zwischen Empfang des Antrags und Abschluss der Formatvalidierung. Engpassindikator bei hohem Antragsaufkommen. | < 1 Sekunde |
| **Vollständigkeit prüfen** (Portal) → **Antragsdaten an Fachverfahren übermitteln** (Portal) | **Portal-Verarbeitungszeit** | Gesamtdauer der Portal-internen Verarbeitungskette bis zur Übermittlung. | < 3 Sekunden |
| **Antragsdaten an Fachverfahren übermitteln** (Portal) → **Antragsdaten auf Plausibilität validieren** (Fachverfahren) | **Übertragungslatenz Portal→Fachverfahren** | Zeitdifferenz zwischen Versand und Empfang der XBau-Nachricht. Indikator für Schnittstellen-Performance. | < 2 Sekunden |
| **Flurstücksdaten anfordern** (Fachverfahren) → **Flurstücksdaten übernehmen** (Fachverfahren) | **Kataster-Antwortzeit** | Wartezeit des Fachverfahrens auf die Flurstücksdaten des GIS-Systems. Kritischer Wartezeittreiber im Prozess. | < 10 Sekunden |
| **Bebauungsplan-Konformität prüfen** (Fachverfahren) → **Baugebühr berechnen** (Fachverfahren) | **Prüf- und Berechnungszeit** | Dauer der fachlichen Kernverarbeitung (Konformitätsprüfung + Gebührenberechnung). Relevant für Kapazitätsplanung. | < 5 Sekunden |
| **Baugenehmigungsbescheid generieren** (Fachverfahren) → **Bescheid an DMS übermitteln** (Fachverfahren) | **Bescheiderstellungszeit** | Dauer der Dokumentengenerierung (PDF/A) bis zur Übermittlung an das DMS. | < 3 Sekunden |
| **Bescheid empfangen** (DMS) → **Dokument archivieren** (DMS) | **Archivierungszeit** | Dauer zwischen Eingang des Bescheids im DMS und abgeschlossener revisionssicherer Archivierung. | < 5 Sekunden |
| **Dokument archivieren** (DMS) → **Baugenehmigung bereitstellen** (DMS) | **Time-to-Availability** | Dauer zwischen Archivierung und Bereitstellung der Baugenehmigung im Portal für den Bauherrn. | < 2 Sekunden |

---

## Eingesetzte IT-Systeme

| System | Rolle im Prozess | Relevante Standards/Komponenten |
| :--- | :--- | :--- |
| **Bauantrags-Portal** | Empfang und Vorverarbeitung digital eingereichter Bauanträge inkl. Anlagen; Eingabevalidierung; Weiterleitung an Fachverfahren | REST-API, XBau |
| **Fachverfahren Bauaufsicht** | Fachliche Prüfung des Bauantrags, Anreicherung mit Flurstücksdaten, Bebauungsplanprüfung, Gebührenberechnung, Bescheiderstellung | XBau, interne Antrags-/Bescheiddatenbank |
| **Liegenschaftskataster/GIS-System** | Bereitstellung amtlicher Flurstücks- und Geodaten für die fachliche Prüfung | ALKIS |
| **Dokumenten-Management-System (DMS)** | Indexierung, revisionssichere Archivierung und Bereitstellung des Baugenehmigungsbescheids | PDF/A, Metadatenindex |

---

## Sicherheitsanforderungen

| Anforderung | Maßnahme |
| :--- | :--- |
| **Authentifizierung** | Alle System-zu-System-Aufrufe erfordern OAuth 2.0 Bearer Tokens bzw. Mutual-TLS-Zertifikate |
| **Autorisierung** | Rollenbasierte Zugriffskontrolle je Fachverfahren (Bauaufsicht, Katasteramt, Registratur) |
| **Transportverschlüsselung** | TLS 1.2+ für alle Schnittstellen zwischen Portal, Fachverfahren, GIS und DMS |
| **Eingabevalidierung** | Strikte Schema-Validierung der XBau- und ALKIS-Nachrichten vor Weiterverarbeitung |
| **Audit-Trail** | Protokollierung aller Statusänderungen des Antrags (Wer, Was, Wann) im Fachverfahren |
| **Revisionssicherheit** | Unveränderbare, indexierte Archivierung des Baugenehmigungsbescheids im DMS (PDF/A) |

---

## Fehlerszenarien & Fallback-Strategien

| Fehlerszenario | Betroffener Pool | Auswirkung | Fallback |
| :--- | :--- | :--- | :--- |
| Formatfehler in Antragsdaten | Bauantrags-Portal | Prozess bricht ab | HTTP 400 an Einreichenden; Antrag verbleibt im Portal zur Korrektur |
| Fehlende Pflichtanlage (z. B. Lageplan) | Bauantrags-Portal | Prozess bricht ab | HTTP 422; Status `unvollständig`, Nachforderung erforderlich |
| Flurstücksnummer im Kataster nicht auffindbar | Liegenschaftskataster/GIS | Prozess pausiert | Fehlermeldung an Fachverfahren; manuelle Prüfung durch Katasteramt |
| Nachrichtenübertragung fehlgeschlagen (Timeout) | Alle Übergänge | Nachricht geht verloren | Retry-Mechanismus (3×, 30s); danach manuelle Eskalation |
| Bebauungsplan nicht konform | Fachverfahren Bauaufsicht | Kein Bescheid im Standardpfad | Weiterleitung an manuelle Sachbearbeitung (außerhalb Happy Path) |
| Archivierungsfehler im DMS | Dokumenten-Management-System | Bescheid nicht abrufbar | Retry der Archivierung; Eskalation an DMS-Administration bei Dauerfehler |

---

## Referenzdokumente

- **BPMN-Modell:** `CreateBPMN/IT_Datenverarbeitung_Baugenehmigung_anmelden.bpmn`
- **XBau-Standard:** XÖV-Spezifikation für den Datenaustausch im Bauantragsverfahren
- **ALKIS-Datenmodell:** Amtliches Liegenschaftskatasterinformationssystem – Objektartenkatalog
- **Landesbauordnung (LBO):** Rechtsgrundlage für Bauantragsverfahren und Bebauungsplanprüfung
- **OZG (Onlinezugangsgesetz):** Rechtsgrundlage für die digitale Antragstellung über das Bauantrags-Portal
- **Steckbrief-Template:** `Steckbrief_Template.md`
