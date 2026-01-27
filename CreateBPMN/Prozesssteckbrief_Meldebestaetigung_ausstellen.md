# Prozesssteckbrief: Meldebestätigung ausstellen

## Zusammenfassung
Der Prozess **"Meldebestätigung ausstellen"** beginnt mit dem Eingang eines Bürgerantrags auf Ausstellung einer Meldebestätigung und führt über die IT-gestützte Identitätsprüfung sowie den Abruf der Meldedaten aus dem Melderegister zur fachlichen Freigabe durch die Behörde und anschließenden automatisierten Dokumentenerzeugung. Er endet mit der digitalen Zustellung der signierten Meldebestätigung an den antragstellenden Bürger über das Online-Postfach. Ziel ist die effiziente, transparente und rechtssichere Ausstellung von Meldebestätigungen bei hoher Servicequalität und größtmöglicher Automatisierung.

## Stammdaten
| Attribut | Wert |
| :--- | :--- |
| **Prozessname** | Meldebestätigung ausstellen |
| **Prozesskategorie** | Bürgerdienste / Meldewesen |
| **Auslöser** | Antrag auf Meldebestätigung eingegangen |
| **Ergebnis** | Meldebestätigung ausgestellt |
| **Hauptverantwortung** | Bürgeramt / Einwohnermeldeamt (fachliche Freigabe und Ausstellung) |
| **Beteiligte Rollen** | Bürger, IT (Serviceportal/Integrationsplattform), Behörde (Bürgeramt/Einwohnermeldeamt) |

## Prozessziele
1. **Effizienz (Durchlaufzeit):** Minimierung der End-to-End-Durchlaufzeit durch automatisierte Datenvalidierung, Authentifizierung und Dokumentgenerierung auf unter 2 Werktage.
2. **Qualität (Daten- und Dokumentqualität):** Sicherstellung korrekter und vollständiger Meldebestätigungen durch automatisierten Registerabgleich und standardisierte Dokumentengenerierung mit qualifizierter elektronischer Signatur.
3. **Rechtssicherheit & Datenschutz:** Einhaltung der Vorgaben des Bundesmeldegesetzes (BMG) sowie der DSGVO durch nachvollziehbare Zugriffskontrollen, revisionssichere Protokollierung und zweckgebundene Verarbeitung.
4. **Serviceorientierung & Transparenz:** Bereitstellung eines medienbruchfreien, digital nachvollziehbaren Antrags- und Zustellwegs über Online-Postfach mit Status-Tracking und automatisierten Benachrichtigungen.

## Key Performance Indicators (KPIs)

Die folgenden Kennzahlen dienen der Messung der Prozessleistung und werden in Prozess-KPIs (Gesamtbetrachtung) und Aktivitaets-KPIs (Schrittbetrachtung) unterteilt.

### 1. Prozess-KPIs (Ebene Gesamtprozess)

Diese KPIs messen den Erfolg des gesamten End-to-End-Prozesses.

| KPI-ID | Kennzahl | Beschreibung | Zielwert | Messmethode |
| :--- | :--- | :--- | :--- | :--- |
| **P-KPI-01** | **End-to-End-Durchlaufzeit** | Gesamtdauer vom Prozessstart (Antrag eingegangen) bis zur Verfügbarkeit der Meldebestätigung im Online-Postfach des Bürgers. Misst die Gesamtgeschwindigkeit der Bearbeitung. | ≤ 2 Werktage | Timestamp(EndEvent_Buerger) - Timestamp(StartEvent_Buerger) |
| **P-KPI-02** | **First-Pass-Yield** | Anteil der Anträge, die ohne Rückfragen oder manuelle Korrekturen durchlaufen können (vollständig, valide, authentifiziert). Indikator für Formularqualität und Automatisierungsgrad. | ≥ 97% | Anzahl(Vorgänge ohne Rückfrage/Fehler) / Gesamtanzahl(Vorgänge) |
| **P-KPI-03** | **SLA-Einhaltungsquote** | Anteil der Vorgänge, die innerhalb des vereinbarten Service Level Agreements (2 Werktage) abgeschlossen werden. | ≥ 95% | Anzahl(Vorgänge innerhalb SLA) / Gesamtanzahl(Vorgänge) |
| **P-KPI-04** | **Digitalquote** | Anteil der Meldebestätigungen, die vollständig digital (Online-Antrag + digitale Zustellung) durchlaufen werden. Indikator für Digitalisierungsgrad. | ≥ 90% | Anzahl(vollständig digital) / Gesamtanzahl(ausgestellt) |

### 2. Aktivitaets-KPIs (Ebene Prozessschritte)

Diese KPIs sind spezifischen Aktivitaeten oder Phasen im BPMN-Modell zugeordnet, um Engpaesse zu identifizieren.

| Zugeordnete Aktivitaet(en) | KPI-Name | Beschreibung & Relevanz | Zielwert |
| :--- | :--- | :--- | :--- |
| **Antrag stellen** (Buerger)  **Antrag entgegennehmen** (IT) | **Time-to-Ingestion** | Zeit bis der Antrag nach Absenden technisch angenommen und als Vorgang angelegt ist. Kritisch fuer Nutzererlebnis und Vermeidung von Doppelantraegen. | < 2 Minuten |
| **Antrag entgegennehmen** (IT)  **Identitaet authentifizieren** (IT) | **Auth-Completion-Time** | Dauer der digitalen Authentifizierung (z. B. eID/Servicekonto). Engpass, da Abbruch- und Fehlerquelle. | < 5 Minuten |
| **Identitaet authentifizieren** (IT)  **Meldedaten abrufen** (IT) | **Register-Query-Latency** | Zeit fuer Registerabfrage und Antwort. Relevanz fuer technische Performance und Verfuegbarkeit. | < 30 Sekunden |
| **Meldedaten abrufen** (IT)  **Ausstellung freigeben** (Behoerde) | **Time-to-Review** | Zeit bis zur fachlichen Freigabe (manueller Schritt). Engpassindikator fuer Kapazitaeten der Sachbearbeitung. | < 8 Stunden (innerhalb Dienstzeit) |
| **Ausstellung freigeben** (Behoerde)  **Meldebestaetigung erzeugen und zustellen** (IT) | **Time-to-Generate** | Zeit vom Freigabezeitpunkt bis zur erfolgreichen Dokumenterzeugung inkl. Siegel/Signatur. | < 10 Minuten |
| **Meldebestaetigung erzeugen und zustellen** (IT)  **Meldebestaetigung empfangen** (Buerger) | **Time-to-Delivery** | Zeit bis die Meldebestaetigung im Postfach zum Download verfuegbar ist bzw. Benachrichtigung erfolgt. | < 15 Minuten |
| **Meldebestaetigung erzeugen und zustellen** (IT) | **Dokument-Fehlerquote** | Anteil fehlgeschlagener Generierungen (z. B. Template-/Siegel-/Ablagefehler). Relevanz fuer Nacharbeit und SLA. | < 0,5% |

## Eingesetzte IT-Systeme
- **Bürgerportal / Online-Formular:** Erfassung und Übermittlung des Antrags mit integrierter Pflichtfeldvalidierung, Plausibilitätsprüfungen und Nutzerführung.
- **Identitätsdienst (BundID / eID / Servicekonto):** Sichere Authentifizierung des Antragstellers und Absicherung des Zugriffs auf personenbezogene Meldedaten gemäß DSGVO.
- **Melderegister / Einwohnermeldewesen-Fachverfahren:** Führendes System für aktuelle und historische Meldedaten, inkl. Adressdaten und Meldehistorie.
- **Dokumentengenerierungsdienst:** Automatisierte Erzeugung der Meldebestätigung (PDF) auf Basis standardisierter Vorlagen mit Datenbefüllung aus dem Melderegister.
- **Signatur-/Siegeldienst:** Anbringung qualifizierter elektronischer Signatur oder Behördensiegel auf die Meldebestätigung zur Gewährleistung der Authentizität.
- **Online-Postfach / Zustellinfrastruktur:** Digitale Bereitstellung der Meldebestätigung, Push-Benachrichtigung an Bürger und rechtsverbindlicher Zustellnachweis.
- **DMS / Vorgangsarchiv:** Revisionssichere, DSGVO-konforme Ablage der Anträge, Protokolle und ausgestellten Dokumente mit Aufbewahrungsfristen.

## Referenzdokumente
- **BPMN-Modell:** `CreateBPMN/Meldebestaetigung_ausstellen.bpmn`
- **Antragsformular:** `forms/Meldebestaetigung_Antrag.form`
- **Rechtliche Grundlagen:**
  - Bundesmeldegesetz (BMG), insbesondere § 34 BMG (Melderegisterauskünfte)
  - Datenschutz-Grundverordnung (DSGVO), Art. 6 Abs. 1 lit. c (Rechtmäßigkeit der Verarbeitung)
  - eIDAS-Verordnung (elektronische Identifizierung und Vertrauensdienste)
- **Interne Regelungen:**
  - Dienstanweisung zur elektronischen Ausstellung von Meldebestätigungen
  - Datenschutzkonzept für das Meldewesen