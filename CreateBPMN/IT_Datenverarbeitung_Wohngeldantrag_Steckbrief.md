# Prozess-Steckbrief: IT-Datenverarbeitung Wohngeldantrag

## Kurze Zusammenfassung

Der Prozess beschreibt die IT-seitige Datenverarbeitung eines Wohngeldantrags von der Datenerfassung über die Validierung, Prüfung und Berechnung bis zur Speicherung im Fachverfahren und der automatisierten Benachrichtigung. Die beteiligten IT-Systeme sind das Online-Formular-Frontend, der Validierungsservice, das Berechnungsmodul, das Wohngeld-Fachverfahren und der Notification-Service. Der Prozess umfasst 18 detaillierte Verarbeitungsschritte, die den gesamten Datenfluss von der Eingabe bis zur Statusaktualisierung abbilden.

---

## Detaillierte Prozessbeschreibung

### Startereignis

**Name**: Antragsdaten empfangen

- **Trigger-Art**: Nachricht (Message-Event)
- **Datenquelle**: Online-Formular des Bürgerportals (Web-Frontend)
- **Datenformat**: JSON
- **Beispiel-Input**: 
  - Antragsteller-Daten (Name, Vorname, Geburtsdatum, Adresse)
  - Haushaltsmitglieder (Anzahl, Alter, Einkommen)
  - Wohnsituation (Miete, Wohnfläche, Anzahl Räume)
  - Einkommensnachweise (Bruttogehalt, Abzüge)
  - Bankverbindung (IBAN, BIC)

---

### Prozessschritte

#### Schritt 1: JSON-Struktur validieren

**Verarbeitendes System**
- Akteur: Validierungsservice
- Typ: Microservice

**Datenverarbeitungsdetails**
- **Input**: JSON-Objekt mit Antragsdaten aus Online-Formular (Raw-Format)
- **Verarbeitungslogik**:
  - Validierung: JSON-Schema-Validierung gegen definiertes Schema (WohngeldAntragV1.json), Prüfung auf wohlgeformtes JSON, Prüfung auf Vollständigkeit der Hauptknoten (antragsteller, haushalt, wohnung, einkommen, bankverbindung)
  - Transformation: Keine
  - Anreicherung: Keine
  - Filterung: Keine
- **Output**: Validierungsergebnis (valid: true/false) mit Liste der Validierungsfehler bei Strukturfehlern
- **Persistierung**: Validierungsprotokoll in Log-Datenbank (MongoDB, Collection: validation_logs)

**Datenaustausch & Integration**
- **Notation**: Online-Formular → Validierungsservice → JSON-Schema-Validator
- **Schnittstelle**: REST-API (POST /api/v1/validate/structure)
- **Protokoll**: HTTPS
- **Datenfluss-Richtung**: Web-Frontend → Validierungsservice

**Technische Abhängigkeiten**
- JSON-Schema-Repository (Version WohngeldAntragV1.json)
- Log-Datenbank (MongoDB) für Audit-Trail

---

#### Schritt 2: Pflichtfelder pruefen

**Verarbeitendes System**
- Akteur: Validierungsservice (Pflichtfeld-Modul)
- Typ: Microservice

**Datenverarbeitungsdetails**
- **Input**: Strukturvalidiertes JSON-Objekt
- **Verarbeitungslogik**:
  - Validierung: Prüfung auf Pflichtfelder (antragsteller.name, antragsteller.vorname, antragsteller.geburtsdatum, antragsteller.adresse, haushalt.anzahl_personen, wohnung.miete, einkommen.gesamt, bankverbindung.iban)
  - Transformation: Keine
  - Anreicherung: Hinzufügen von Validierungs-Flags pro Feld (field_valid: true/false)
  - Filterung: Keine
- **Output**: Validiertes JSON-Objekt mit Pflichtfeld-Status
- **Persistierung**: Validierungsdetails in Log-Datenbank (MongoDB, Collection: field_validations)

**Datenaustausch & Integration**
- **Notation**: Validierungsservice (Struktur) → Validierungsservice (Pflichtfeld)
- **Schnittstelle**: Interner Service-Call (in-memory)
- **Protokoll**: N/A (interne Verarbeitung)
- **Datenfluss-Richtung**: Struktur-Validator → Pflichtfeld-Validator

**Technische Abhängigkeiten**
- Pflichtfeld-Konfiguration (YAML-Datei: required_fields.yml)
- Log-Datenbank (MongoDB)

---

#### Schritt 3: Datenformate validieren

**Verarbeitendes System**
- Akteur: Validierungsservice (Format-Validierungs-Modul)
- Typ: Microservice

**Datenverarbeitungsdetails**
- **Input**: Pflichtfeld-validiertes JSON-Objekt
- **Verarbeitungslogik**:
  - Validierung: Format-Checks (Geburtsdatum: YYYY-MM-DD, E-Mail: RFC 5322, Telefon: E.164, PLZ: 5-stellig numerisch, Miete/Einkommen: Dezimalzahl mit max. 2 Nachkommastellen)
  - Transformation: Normalisierung von Datumsformaten, Bereinigung von Leerzeichen bei numerischen Feldern
  - Anreicherung: Hinzufügen von Format-Validierungs-Status
  - Filterung: Keine
- **Output**: Format-validiertes JSON-Objekt
- **Persistierung**: Format-Validierungsprotokoll in Log-Datenbank (MongoDB, Collection: format_validations)

**Datenaustausch & Integration**
- **Notation**: Validierungsservice (Pflichtfeld) → Validierungsservice (Format)
- **Schnittstelle**: Interner Service-Call
- **Protokoll**: N/A (interne Verarbeitung)
- **Datenfluss-Richtung**: Pflichtfeld-Validator → Format-Validator

**Technische Abhängigkeiten**
- Format-Validierungs-Bibliothek (validator.js v13.x)
- Regex-Pattern-Repository
- Log-Datenbank (MongoDB)

---

#### Schritt 4: IBAN validieren

**Verarbeitendes System**
- Akteur: Validierungsservice (IBAN-Validierungs-Modul)
- Typ: Microservice mit externer API-Anbindung

**Datenverarbeitungsdetails**
- **Input**: Format-validiertes JSON-Objekt mit IBAN-Feld
- **Verarbeitungslogik**:
  - Validierung: IBAN-Format-Prüfung (Länge, Ländercode, Prüfziffer nach ISO 13616), Prüfung auf gültige Bankleitzahl (BIC-Lookup)
  - Transformation: Entfernung von Leerzeichen in IBAN, Konvertierung zu Großbuchstaben
  - Anreicherung: Hinzufügen von Bank-Informationen (Bankname, BIC) aus IBAN-Lookup
  - Filterung: Keine
- **Output**: IBAN-validiertes JSON-Objekt mit angereicherten Bank-Informationen
- **Persistierung**: IBAN-Validierungsprotokoll in Log-Datenbank (MongoDB, Collection: iban_validations)

**Datenaustausch & Integration**
- **Notation**: Validierungsservice (Format) → IBAN-Validierungs-API → Bankdatenbank
- **Schnittstelle**: REST-API (GET /api/v1/iban/validate/{iban})
- **Protokoll**: HTTPS
- **Datenfluss-Richtung**: Format-Validator → IBAN-Validator → Bundesbank IBAN-Registry

**Technische Abhängigkeiten**
- IBAN-Validierungs-Bibliothek (iban-tools v4.x)
- Bundesbank IBAN-Registry (externe API)
- BIC-Datenbank (lokal gecacht)

---

#### Schritt 5: Stammdaten Antragsteller abrufen

**Verarbeitendes System**
- Akteur: Stammdaten-Service
- Typ: Service mit Datenbankzugriff

**Datenverarbeitungsdetails**
- **Input**: Validiertes Antragsdaten-Objekt mit Antragsteller-Identifikation (Name, Geburtsdatum, Adresse)
- **Verarbeitungslogik**:
  - Validierung: Prüfung auf Existenz des Antragstellers in Stammdatensystem (Matching-Score berechnen)
  - Transformation: Keine
  - Anreicherung: Abruf von Stammdaten (Personennummer, historische Anträge, aktuelle Leistungsbezüge, Meldeadresse)
  - Filterung: Nur relevante Stammdaten für Wohngeldberechnung
- **Output**: Angereicherte Antragsdaten mit Stammdaten-Informationen
- **Persistierung**: Keine (Read-Only-Zugriff auf Stammdatenbank)

**Datenaustausch & Integration**
- **Notation**: Validierungsservice → Stammdaten-Service → Stammdatenbank
- **Schnittstelle**: REST-API (POST /api/v1/stammdaten/query)
- **Protokoll**: HTTPS mit OAuth2-Token
- **Datenfluss-Richtung**: Validierungsservice → Stammdaten-Service → PostgreSQL-Stammdatenbank

**Technische Abhängigkeiten**
- Stammdatenbank (PostgreSQL, Schema: buerger_stammdaten)
- OAuth2-Authentifizierungs-Server
- Matching-Algorithmus (Fuzzy-String-Matching)

---

#### Schritt 6: Mietstufe ermitteln

**Verarbeitendes System**
- Akteur: Berechnungsmodul (Mietstufen-Ermittlung)
- Typ: Service

**Datenverarbeitungsdetails**
- **Input**: Angereicherte Antragsdaten mit Wohnadresse
- **Verarbeitungslogik**:
  - Validierung: Prüfung auf gültige PLZ und Gemeindeschlüssel
  - Transformation: Mapping PLZ → Gemeindeschlüssel (8-stellig)
  - Anreicherung: Abruf Mietstufe (I-VII) aus Mietstufen-Tabelle basierend auf Gemeindeschlüssel
  - Filterung: Keine
- **Output**: Antragsdaten mit ermittelter Mietstufe
- **Persistierung**: Keine

**Datenaustausch & Integration**
- **Notation**: Stammdaten-Service → Berechnungsmodul → Parameterdatenbank (Mietstufen)
- **Schnittstelle**: SQL-Query (SELECT mietstufe FROM mietstufen_tabelle WHERE gemeindeschluessel = ?)
- **Protokoll**: PostgreSQL-Datenbankprotokoll
- **Datenfluss-Richtung**: Berechnungsmodul → Parameterdatenbank

**Technische Abhängigkeiten**
- Parameterdatenbank (PostgreSQL, Tabelle: mietstufen_tabelle)
- PLZ-Gemeindeschlüssel-Mapping (Tabelle: plz_gemeinde_mapping)
- Aktuelle Mietstufen nach WoGG (jährlich aktualisiert)

---

#### Schritt 7: Haushaltsgroesse berechnen

**Verarbeitendes System**
- Akteur: Berechnungsmodul (Haushalts-Analyse)
- Typ: Service

**Datenverarbeitungsdetails**
- **Input**: Antragsdaten mit Haushaltsmitglieder-Informationen
- **Verarbeitungslogik**:
  - Validierung: Prüfung auf Konsistenz der Haushaltsmitglieder-Angaben
  - Transformation: Berechnung Haushaltsgröße (Anzahl Personen im Haushalt), Kategorisierung nach Alter (Kinder < 18, Erwachsene >= 18)
  - Anreicherung: Hinzufügen von Haushaltsgröße und Altersstruktur
  - Filterung: Keine
- **Output**: Antragsdaten mit berechneter Haushaltsgröße
- **Persistierung**: Keine

**Datenaustausch & Integration**
- **Notation**: Berechnungsmodul (intern)
- **Schnittstelle**: Interne Berechnung
- **Protokoll**: N/A
- **Datenfluss-Richtung**: Interne Verarbeitung

**Technische Abhängigkeiten**
- Haushaltsgrößen-Berechnungslogik (nach §5 WoGG)

---

#### Schritt 8: Einkommensgrenzen abrufen

**Verarbeitendes System**
- Akteur: Berechnungsmodul (Einkommensgrenzen-Service)
- Typ: Service

**Datenverarbeitungsdetails**
- **Input**: Antragsdaten mit Haushaltsgröße und Mietstufe
- **Verarbeitungslogik**:
  - Validierung: Keine
  - Transformation: Keine
  - Anreicherung: Abruf aktueller Einkommensgrenzen aus Parametertabelle (abhängig von Haushaltsgröße und Mietstufe)
  - Filterung: Keine
- **Output**: Antragsdaten mit Einkommensgrenzen
- **Persistierung**: Keine

**Datenaustausch & Integration**
- **Notation**: Berechnungsmodul → Parameterdatenbank (Einkommensgrenzen)
- **Schnittstelle**: SQL-Query (SELECT einkommensgrenze FROM einkommensgrenzen WHERE haushaltsgroesse = ? AND mietstufe = ?)
- **Protokoll**: PostgreSQL-Datenbankprotokoll
- **Datenfluss-Richtung**: Berechnungsmodul → Parameterdatenbank

**Technische Abhängigkeiten**
- Parameterdatenbank (PostgreSQL, Tabelle: einkommensgrenzen)
- Aktuelle Einkommensgrenzen nach WoGG (jährlich aktualisiert)

---

#### Schritt 9: Einkommen gegen Grenzwerte pruefen

**Verarbeitendes System**
- Akteur: Berechnungsmodul (Einkommensprüfung)
- Typ: Service

**Datenverarbeitungsdetails**
- **Input**: Antragsdaten mit Gesamteinkommen und Einkommensgrenzen
- **Verarbeitungslogik**:
  - Validierung: Prüfung ob Gesamteinkommen <= Einkommensgrenze (Happy Path: Bedingung erfüllt)
  - Transformation: Berechnung des Gesamteinkommens (Summe aller Haushaltseinkommen abzüglich Freibeträge)
- Anreicherung: Hinzufügen von Prüfergebnis (berechtigt: true/false) und Freibeträge
  - Filterung: Keine
- **Output**: Antragsdaten mit Einkommensprüfungs-Ergebnis
- **Persistierung**: Keine

**Datenaustausch & Integration**
- **Notation**: Berechnungsmodul (intern)
- **Schnittstelle**: Interne Berechnung
- **Protokoll**: N/A
- **Datenfluss-Richtung**: Interne Verarbeitung

**Technische Abhängigkeiten**
- Einkommensprüfungs-Logik nach §14 WoGG
- Freibeträge-Tabelle (Parameterdatenbank)

---

#### Schritt 10: Wohngeldformel anwenden

**Verarbeitendes System**
- Akteur: Berechnungsmodul (Wohngeld-Engine)
- Typ: Service

**Datenverarbeitungsdetails**
- **Input**: Antragsdaten mit Haushaltsgröße, Einkommen, Miete, Mietstufe
- **Verarbeitungslogik**:
  - Validierung: Keine
  - Transformation: Anwendung der Wohngeldformel nach §19 WoGG: W = M - (a + b × M + c × Y) × M
    - M = zu berücksichtigende Miete
    - Y = monatliches Gesamteinkommen
    - a, b, c = Formelwerte abhängig von Haushaltsgröße
  - Anreicherung: Hinzufügen von Formelwerten und Zwischenergebnissen
  - Filterung: Keine
- **Output**: Antragsdaten mit Wohngeld-Rohbetrag
- **Persistierung**: Keine

**Datenaustausch & Integration**
- **Notation**: Berechnungsmodul → Parameterdatenbank (Formelwerte)
- **Schnittstelle**: SQL-Query (SELECT a, b, c FROM wohngeldformel WHERE haushaltsgroesse = ?)
- **Protokoll**: PostgreSQL-Datenbankprotokoll
- **Datenfluss-Richtung**: Berechnungsmodul → Parameterdatenbank

**Technische Abhängigkeiten**
- Parameterdatenbank (PostgreSQL, Tabelle: wohngeldformel)
- Wohngeldformel-Implementierung (Math-Library)

---

#### Schritt 11: Anspruchsbetrag berechnen

**Verarbeitendes System**
- Akteur: Berechnungsmodul (Anspruchsberechnung)
- Typ: Service

**Datenverarbeitungsdetails**
- **Input**: Antragsdaten mit Wohngeld-Rohbetrag
- **Verarbeitungslogik**:
  - Validierung: Prüfung auf Mindestbetrag (> 10 EUR)
  - Transformation: Rundung auf volle Euro (kaufmännisch), Anwendung von Höchstbeträgen
  - Anreicherung: Hinzufügen von finalem Anspruchsbetrag
  - Filterung: Keine
- **Output**: Antragsdaten mit finalem monatlichen Wohngeldanspruch
- **Persistierung**: Keine

**Datenaustausch & Integration**
- **Notation**: Berechnungsmodul (intern)
- **Schnittstelle**: Interne Berechnung
- **Protokoll**: N/A
- **Datenfluss-Richtung**: Interne Verarbeitung

**Technische Abhängigkeiten**
- Rundungsregeln nach WoGG
- Höchstbetrags-Tabelle (Parameterdatenbank)

---

#### Schritt 12: Bewilligungszeitraum festlegen

**Verarbeitendes System**
- Akteur: Berechnungsmodul (Zeitraum-Service)
- Typ: Service

**Datenverarbeitungsdetails**
- **Input**: Antragsdaten mit Antragsdatum
- **Verarbeitungslogik**:
  - Validierung: Keine
  - Transformation: Berechnung Bewilligungszeitraum (Standard: 12 Monate ab Antragsmonat), Berechnung Bewilligungszeitraum-Ende
  - Anreicherung: Hinzufügen von Bewilligungszeitraum (von-bis)
  - Filterung: Keine
- **Output**: Antragsdaten mit Bewilligungszeitraum
- **Persistierung**: Keine

**Datenaustausch & Integration**
- **Notation**: Berechnungsmodul (intern)
- **Schnittstelle**: Interne Berechnung (Date-Calculation)
- **Protokoll**: N/A
- **Datenfluss-Richtung**: Interne Verarbeitung

**Technische Abhängigkeiten**
- Date-Calculation-Library (moment.js)
- Bewilligungszeitraum-Regeln nach §25 WoGG

---

#### Schritt 13: Antragsdaten speichern

**Verarbeitendes System**
- Akteur: Wohngeld-Fachverfahren (Datenbank-Service)
- Typ: Datenbank-Service mit Transaktionsmanagement

**Datenverarbeitungsdetails**
- **Input**: Vollständige Antragsdaten inkl. aller Berechnungen
- **Verarbeitungslogik**:
  - Validierung: Transaktionsprüfung (ACID-Eigenschaften), Duplikatsprüfung (kein identischer Antrag vorhanden)
  - Transformation: Mapping JSON-Struktur auf relationales Datenbankschema (Tabellen: antrag, antragsteller, haushaltsmitglieder)
  - Anreicherung: Generierung Antragsnummer (UUID v4), Zeitstempel (created_at, updated_at), Status-Flag (eingegangen)
  - Filterung: Keine
- **Output**: Persistierte Antragsdaten mit Antragsnummer
- **Persistierung**: PostgreSQL-Datenbank (Schema: wohngeld), Tabellen: antrag, antragsteller, haushaltsmitglieder

**Datenaustausch & Integration**
- **Notation**: Berechnungsmodul → Wohngeld-Fachverfahren-Datenbank
- **Schnittstelle**: REST-API (POST /api/v1/antrag/speichern)
- **Protokoll**: HTTPS mit JWT-Authentifizierung
- **Datenfluss-Richtung**: Berechnungsmodul → Wohngeld-Fachverfahren-Datenbank

**Technische Abhängigkeiten**
- PostgreSQL-Datenbank (Wohngeld-Schema, Version 14.x)
- JWT-Authentifizierungs-Service
- UUID-Generator (uuid v4)

---

#### Schritt 14: Berechnungsergebnis speichern

**Verarbeitendes System**
- Akteur: Wohngeld-Fachverfahren (Berechnungs-Persistierung)
- Typ: Datenbank-Service

**Datenverarbeitungsdetails**
- **Input**: Berechnungsergebnisse (Wohngeldanspruch, Bewilligungszeitraum, Formelwerte)
- **Verarbeitungslogik**:
  - Validierung: Transaktionsprüfung, Referenzintegrität zu Antragsdatensatz
  - Transformation: Mapping Berechnungsdaten auf Datenbankschema (Tabelle: berechnung)
  - Anreicherung: Hinzufügen von Berechnungs-Metadaten (Berechnungsdatum, verwendete Formelversion, Parameterstände)
  - Filterung: Keine
- **Output**: Persistierte Berechnungsergebnisse
- **Persistierung**: PostgreSQL-Datenbank (Schema: wohngeld, Tabelle: berechnung)

**Datenaustausch & Integration**
- **Notation**: Wohngeld-Fachverfahren (intern)
- **Schnittstelle**: SQL-INSERT (INSERT INTO berechnung ...)
- **Protokoll**: PostgreSQL-Datenbankprotokoll
- **Datenfluss-Richtung**: Interne Datenbank-Transaktion

**Technische Abhängigkeiten**
- PostgreSQL-Datenbank (Foreign Key zu antrag.id)
- Transaktionsmanagement (ACID)

---

#### Schritt 15: Vorgangsnummer generieren

**Verarbeitendes System**
- Akteur: Vorgangs-Service
- Typ: Service

**Datenverarbeitungsdetails**
- **Input**: Antragsnummer (UUID)
- **Verarbeitungslogik**:
  - Validierung: Keine
  - Transformation: Generierung sprechender Vorgangsnummer (Format: WG-YYYY-MM-NNNNNN, z.B. WG-2025-11-000123)
  - Anreicherung: Mapping UUID → Vorgangsnummer
  - Filterung: Keine
- **Output**: Vorgangsnummer
- **Persistierung**: Update in Datenbank (Tabelle: antrag, Feld: vorgangsnummer)

**Datenaustausch & Integration**
- **Notation**: Wohngeld-Fachverfahren → Vorgangs-Service → Datenbank
- **Schnittstelle**: REST-API (POST /api/v1/vorgang/generieren) + SQL-UPDATE
- **Protokoll**: HTTPS + PostgreSQL
- **Datenfluss-Richtung**: Fachverfahren → Vorgangs-Service → Datenbank

**Technische Abhängigkeiten**
- Sequenz-Generator (PostgreSQL Sequence: vorgang_seq)
- Vorgangsnummer-Format-Definition

---

#### Schritt 16: E-Mail-Vorlage generieren

**Verarbeitendes System**
- Akteur: Notification-Service (Template-Engine)
- Typ: Microservice

**Datenverarbeitungsdetails**
- **Input**: Antragsdaten (Vorgangsnummer, Antragsteller-Name, Eingangsdatum, Kontaktdaten)
- **Verarbeitungslogik**:
  - Validierung: E-Mail-Format-Prüfung
  - Transformation: Generierung E-Mail-Body aus Template (Handlebars-Template), Befüllung Platzhalter ({{vorgangsnummer}}, {{name}}, {{datum}})
  - Anreicherung: Hinzufügen Standard-Textbausteine (Bearbeitungszeit: 4-6 Wochen, Kontaktdaten Wohngeldstelle, Hinweis auf Nachreichung fehlender Unterlagen)
  - Filterung: Keine
- **Output**: Formatierte E-Mail (HTML + Plain-Text-Variante)
- **Persistierung**: E-Mail-Template-Cache (Redis)

**Datenaustausch & Integration**
- **Notation**: Wohngeld-Fachverfahren → Notification-Service → Template-Repository
- **Schnittstelle**: REST-API (POST /api/v1/notification/generate-email)
- **Protokoll**: HTTPS
- **Datenfluss-Richtung**: Fachverfahren → Notification-Service → Template-Repository

**Technische Abhängigkeiten**
- Template-Engine (Handlebars.js v4.x)
- E-Mail-Template-Repository (Git-Repository mit Versioning)
- Redis-Cache für Template-Performance

---

#### Schritt 17: Eingangsbestaetigung versenden

**Verarbeitendes System**
- Akteur: Notification-Service (E-Mail-Versand)
- Typ: Send Task / Microservice

**Datenverarbeitungsdetails**
- **Input**: Generierte E-Mail (HTML + Plain-Text), Empfänger-E-Mail-Adresse
- **Verarbeitungslogik**:
  - Validierung: E-Mail-Adresse gültig, E-Mail-Server erreichbar
  - Transformation: Keine
  - Anreicherung: Hinzufügen E-Mail-Header (From, To, Subject, Message-ID, Date)
  - Filterung: Keine
- **Output**: Versendete E-Mail
- **Persistierung**: Versandprotokoll in Log-Datenbank (MongoDB, Collection: email_logs) mit Timestamp, Empfänger, Status (delivered/failed), Message-ID

**Datenaustausch & Integration**
- **Notation**: Notification-Service → E-Mail-Gateway → SMTP-Server → Empfänger
- **Schnittstelle**: SMTP-API
- **Protokoll**: SMTP über TLS (Port 587)
- **Datenfluss-Richtung**: Notification-Service → E-Mail-Gateway → SMTP-Server

**Technische Abhängigkeiten**
- E-Mail-Gateway (SendGrid oder Amazon SES)
- SMTP-Server (TLS-verschlüsselt)
- Retry-Mechanismus bei Zustellfehlern (max. 3 Versuche)

---

#### Schritt 18: Workflow-Status aktualisieren

**Verarbeitendes System**
- Akteur: Workflow-Engine
- Typ: Service

**Datenverarbeitungsdetails**
- **Input**: Antragsnummer, Verarbeitungsergebnis (alle Schritte erfolgreich)
- **Verarbeitungslogik**:
  - Validierung: Prüfung auf gültige Statusübergänge (State-Machine)
  - Transformation: Status-Update von "eingegangen" auf "in_bearbeitung"
  - Anreicherung: Hinzufügen von Workflow-Metadaten (letzter_bearbeiter: "System", bearbeitungsdatum, naechster_schritt: "Dokumentenpruefung")
  - Filterung: Keine
- **Output**: Aktualisierter Workflow-Status
- **Persistierung**: Update in Datenbank (Tabelle: antrag, Feld: workflow_status), Workflow-Historie (Tabelle: workflow_history)

**Datenaustausch & Integration**
- **Notation**: Notification-Service → Workflow-Engine → Datenbank
- **Schnittstelle**: REST-API (PATCH /api/v1/workflow/status/{antragsnummer}) + SQL-UPDATE
- **Protokoll**: HTTPS + PostgreSQL
- **Datenfluss-Richtung**: Notification-Service → Workflow-Engine → Datenbank

**Technische Abhängigkeiten**
- Workflow-State-Machine (definierte Statusübergänge)
- PostgreSQL-Datenbank (Tabellen: antrag, workflow_history)
- Event-Bus für Workflow-Events (RabbitMQ)

---

### Endereignis

**Name**: Antrag verarbeitet

- **Ergebnis-Art**: Daten vollständig verarbeitet und persistent gespeichert, Eingangsbestätigung versendet, Workflow-Status "in_bearbeitung" gesetzt
- **Output-Daten**: 
  - Persistierter Wohngeldantrag in PostgreSQL-Datenbank (Schema: wohngeld)
  - Tabellen: antrag, antragsteller, haushaltsmitglieder, berechnung
  - Antragsnummer (UUID-Format) und Vorgangsnummer (WG-YYYY-MM-NNNNNN)
  - Berechneter Wohngeldanspruch (monatlicher Betrag in EUR)
  - Bewilligungszeitraum (von-bis Datum)
  - Eingangsdatum und Bearbeitungsstatus
- **Nachfolgende Systeme**: 
  - Sachbearbeitungs-Workflow (Zugriff auf gespeicherte Antragsdaten zur Dokumentenprüfung)
  - Bescheid-Erstellungs-System (Nutzung der Berechnungsergebnisse)
  - Reporting-System (Zugriff auf Workflow-Historie und Statistiken)

---

## Technische Zusammenfassung

**Anzahl Tasks**: 18 Service Tasks
**Beteiligte Systeme**: 
- Validierungsservice (4 Tasks)
- Berechnungsmodul (7 Tasks)
- Wohngeld-Fachverfahren (3 Tasks)
- Notification-Service (2 Tasks)
- Vorgangs-Service (1 Task)
- Workflow-Engine (1 Task)

**Datenbanken**:
- PostgreSQL (Stammdaten, Parameterdaten, Wohngeld-Fachverfahren)
- MongoDB (Validierungs- und Versandprotokolle)
- Redis (Template-Cache)

**Externe Schnittstellen**:
- Bundesbank IBAN-Registry (IBAN-Validierung)
- E-Mail-Gateway (SendGrid/Amazon SES)
- OAuth2-Server (Authentifizierung)

**Prozessart**: Happy Path (ohne Fehlerbehandlung und Alternativpfade)
**Durchlaufzeit**: ca. 2-5 Sekunden (bei optimaler Performance)
