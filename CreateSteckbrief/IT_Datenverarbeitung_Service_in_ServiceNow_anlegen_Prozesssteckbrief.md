# Prozesssteckbrief: Service in ServiceNow anlegen

## Zusammenfassung

Der Prozess **„Service in ServiceNow anlegen"** beschreibt die vollautomatisierte, systemübergreifende Anlage eines neuen IT-Services in der ServiceNow-Plattform. Ausgehend von einer eingehenden REST-API-Anfrage über das ServiceNow API Gateway durchläuft der Prozess die vier IT-Subsysteme CMDB, Service Catalog und Notification Service, die als eigenständige Pools in einer BPMN-Kollaboration modelliert sind. Ziel ist die konsistente, revisionssichere Erstellung eines vollständig konfigurierten, genehmigten und im Self-Service-Portal veröffentlichten Services, über dessen Bereitstellung alle relevanten Stakeholder automatisiert benachrichtigt werden.

---

## Stammdaten

| Attribut | Wert |
| :--- | :--- |
| **Prozessname** | Service in ServiceNow anlegen |
| **Prozesskategorie** | IT-Datenverarbeitung / ITSM Service Management |
| **Auslöser** | Serviceanfrage eingegangen (HTTPS POST via REST API) |
| **Ergebnis** | Stakeholder benachrichtigt (Service vollständig angelegt, aktiviert und publiziert) |
| **Prozesstyp** | Vollautomatisierter IT-Hintergrundprozess (keine manuelle Benutzerinteraktion im Standardpfad) |
| **Hauptverantwortung** | ServiceNow Platform Team / IT Service Management |
| **Beteiligte IT-Systeme (Pools)** | ServiceNow API Gateway, ServiceNow CMDB, ServiceNow Service Catalog, ServiceNow Notification Service |
| **Aufgerufene Subsysteme** | ServiceNow AMB (Asynchronous Message Bus), ServiceNow Flow Designer, ServiceNow SMTP Relay |
| **BPMN-Modell** | `IT_Datenverarbeitung_Service_in_ServiceNow_anlegen.bpmn` |
| **Erstellt am** | 11.05.2026 |
| **Version** | 1.0 |

---

## Prozessziele

1. **Automatisierung:** Vollständige Eliminierung manueller Eingriffe im Standardpfad durch End-to-End-Orchestrierung der ServiceNow-Subsysteme via AMB und REST-API.
2. **Datenintegrität:** Sicherstellung konsistenter und vollständiger Datensätze in CMDB (`cmdb_ci_service`), Service Catalog (`sc_cat_item`) und Audit-Log (`sys_audit`) durch transaktionale Datenbankoperationen.
3. **Compliance & Governance:** Einhaltung des ITIL-konformen Approval-Workflows für jeden neuen Service sowie lückenlose Nachvollziehbarkeit durch Audit-Trails in `sys_audit`.
4. **Serviceorientierung:** Automatische Publikation des genehmigten Services im Self-Service-Portal sowie Benachrichtigung aller Stakeholder ohne zusätzlichen manuellen Aufwand.
5. **Skalierbarkeit:** Lose Kopplung der Subsysteme über den AMB ermöglicht unabhängige Skalierung und Wartung einzelner Verarbeitungskomponenten.

---

## Technische Rahmenbedingungen

### Plattform & Infrastruktur

| Parameter | Wert |
| :--- | :--- |
| **Plattform** | ServiceNow (ITSM-Suite, SaaS) |
| **Ausführungsumgebung** | ServiceNow Platform (Now Platform) |
| **API-Protokoll** | REST / JSON über HTTPS (TLS 1.2+) |
| **Interne Kommunikation** | ServiceNow AMB (Asynchronous Message Bus) / WebSocket |
| **Authentifizierung** | OAuth 2.0 (Bearer Token) oder Basic Auth (service account) |
| **Autorisierung** | ServiceNow ACL (Access Control List) auf Tabellen-/Feld-Ebene |
| **Datenbankschema** | ServiceNow Multi-Tenant DB (MySQL / Oracle) |
| **Suchindex** | Elasticsearch (integriert in ServiceNow) |
| **E-Mail-Versand** | SMTP-Relay (TLS-verschlüsselt) |

### API-Endpunkt (Einstiegspunkt)

| Parameter | Wert |
| :--- | :--- |
| **Methode** | `POST` |
| **Endpunkt** | `/api/now/table/cmdb_ci_service` |
| **Content-Type** | `application/json` |
| **Accept** | `application/json` |

**Beispiel-Request-Payload:**
```json
{
  "name": "E-Mail-Service",
  "short_description": "Zentraler E-Mail-Dienst für alle Mitarbeitenden",
  "service_classification": "Business Service",
  "operational_status": "1",
  "owned_by": "a8f98bb0eb32010045e1a5115206fe3a",
  "support_group": "d625dccec0a8016700a222a0f7900d06",
  "business_criticality": "2 - High",
  "used_for": "Production",
  "category": "Communication"
}
```

**Pflichtfelder:**
- `name` (String, max. 255 Zeichen)
- `service_classification` (Choice: `Business Service`, `Technical Service`, `Shared Service`)
- `owned_by` (SysID des Verantwortlichen aus `sys_user`)

---

## Prozessablauf (End-to-End)

### Pool 1 – ServiceNow API Gateway

| Schritt | Aktivität | Typ | Input | Output | ServiceNow-Tabelle(n) |
| :---: | :--- | :--- | :--- | :--- | :--- |
| 1 | Serviceanfrage empfangen | Receive Task | HTTPS POST JSON-Payload | Rohes Datenobjekt im internen Format | – (Session-Cache) |
| 2 | Eingabedaten validieren | Service Task | Rohes Datenobjekt | Validiertes Objekt oder Fehlerantwort (HTTP 400) | `sys_dictionary` (Schema-Referenz) |
| 3 | Service-Kategorie prüfen | Service Task | `service_classification`-Wert | Aufgelöste Kategorie-SysID; angereichertes Objekt | `cmdb_service_category` |
| 4 | CMDB-Erstellung auslösen | Send Task | Vollständiges Datenobjekt | Message `Service-Erstellungsauftrag` an AMB | – (AMB-Queue) |

**Fehlerbehandlung Pool 1:**
- Validierungsfehler → HTTP 400 mit strukturiertem Error-Body (`{ "error": { "message": "...", "detail": "..." }, "status": "failure" }`)
- Unbekannte Kategorie → HTTP 422 (Unprocessable Entity)
- Authentifizierungsfehler → HTTP 401

---

### Pool 2 – ServiceNow CMDB

| Schritt | Aktivität | Typ | Input | Output | ServiceNow-Tabelle(n) |
| :---: | :--- | :--- | :--- | :--- | :--- |
| 5 | Service-Stammdaten anlegen | Service Task | AMB-Nachricht mit Stammdaten | Neuer Datensatz mit generierter `sys_id` (UUID v4) | `cmdb_ci_service` (INSERT) |
| 6 | Service-Attribute konfigurieren | Service Task | `sys_id` + Zusatzattribute | Attribute-befüllter Datensatz | `cmdb_ci_service` (UPDATE) |
| 7 | CI-Abhängigkeiten verknüpfen | Service Task | `sys_id` + `depends_on`-Liste | Relationship-Datensätze | `cmdb_rel_ci` (INSERT) |
| 8 | Service-Datensatz speichern | Service Task | Alle Transaktionsänderungen | Committeter, indexierter Datensatz | `cmdb_ci_service`, `sys_audit` (COMMIT) |
| 9 | Katalog-Eintrag auslösen | Send Task | `sys_id` + Service-Metadaten | Message `Katalog-Registrierungsauftrag` an AMB | – (AMB-Queue) |

**CMDB-Datenbankfelder (Pflicht/Optional):**

| Feldname | Typ | Pflicht | Beschreibung |
| :--- | :--- | :---: | :--- |
| `sys_id` | GUID | ✓ | Systemgenerierte UUID (Primary Key) |
| `name` | String(255) | ✓ | Servicename |
| `service_classification` | Choice | ✓ | Business/Technical/Shared |
| `owned_by` | Reference(sys_user) | ✓ | Verantwortliche Person |
| `support_group` | Reference(sys_user_group) | – | Zuständige Support-Gruppe |
| `operational_status` | Integer | ✓ | 1=Operational, 2=Non-Operational |
| `business_criticality` | Choice | – | 1-Critical bis 4-Low |
| `sys_created_on` | DateTime | ✓ | Systemgenerierter Timestamp |
| `sys_created_by` | String | ✓ | Systemgenerierter Ersteller |

---

### Pool 3 – ServiceNow Service Catalog

| Schritt | Aktivität | Typ | Input | Output | ServiceNow-Tabelle(n) |
| :---: | :--- | :--- | :--- | :--- | :--- |
| 10 | Katalogeintrag erstellen | Service Task | AMB-Nachricht + CMDB-`sys_id` | Neuer Katalogeintrag verknüpft mit CMDB-CI | `sc_cat_item` (INSERT) |
| 11 | SLA-Parameter zuweisen | Service Task | `sc_cat_item`-`sys_id` + Klassifizierung | SLA-Datensatz mit Response/Resolution Time | `contract_sla` (INSERT) |
| 12 | Approval-Workflow starten | Service Task | Katalogeintrag-`sys_id` + Owner-SysID | Approval-Task; Status → `pending_approval` | `sysapproval_approver` (INSERT), `sc_cat_item` (UPDATE) |
| 13 | Genehmigung verarbeiten | Service Task | Approval-Antwort (Status = `approved`) | Freigegebener Approval-Datensatz | `sysapproval_approver` (UPDATE) |
| 14 | Service aktivieren | Service Task | Genehmigte Katalogeintrag-`sys_id` | Aktiver, publizierter Service im Self-Service-Portal | `sc_cat_item` (UPDATE: `active=true`), `cmdb_ci_service` (UPDATE: `operational_status=1`) |
| 15 | Benachrichtigung auslösen | Send Task | Service-Name, Verantwortliche, Aktivierungsdatum | Message `Benachrichtigungsauftrag` an AMB | – (AMB-Queue) |

**SLA-Standardwerte nach Service-Klassifizierung:**

| Service-Klassifizierung | Response Time | Resolution Time | Eskalationsstufen |
| :--- | :--- | :--- | :--- |
| Business Service (Critical) | 1 Stunde | 4 Stunden | P1 → P2 (nach 2h) |
| Business Service (High) | 4 Stunden | 8 Stunden | P2 → P3 (nach 4h) |
| Technical Service | 8 Stunden | 24 Stunden | P3 → P4 (nach 12h) |
| Shared Service | 24 Stunden | 72 Stunden | P4 (nach 48h) |

---

### Pool 4 – ServiceNow Notification Service

| Schritt | Aktivität | Typ | Input | Output | ServiceNow-Tabelle(n) |
| :---: | :--- | :--- | :--- | :--- | :--- |
| 16 | Empfängerliste ermitteln | Service Task | Support-Group-SysID + Owner-SysID | Liste von E-Mail-Adressen | `sys_user_grmember`, `sys_user` (SELECT) |
| 17 | Benachrichtigungsinhalt generieren | Service Task | Service-Metadaten + Empfängerliste | Fertiger E-Mail-Body (HTML + Plaintext) | `sysevent_email_action` (Template-Lookup) |
| 18 | E-Mail-Benachrichtigung versenden | Service Task | E-Mail-Inhalt + Empfängerliste | Versendete E-Mails; Versandprotokoll | `sys_email` (INSERT) |

**E-Mail-Template-Variablen:**

| Variable | Quelle | Beschreibung |
| :--- | :--- | :--- |
| `${service_name}` | `cmdb_ci_service.name` | Name des neuen Services |
| `${service_url}` | ServiceNow Portal Base URL + `sys_id` | Direktlink zum Service-Datensatz |
| `${service_owner}` | `sys_user.name` (resolved) | Vollständiger Name des Service Owners |
| `${activated_on}` | `sc_cat_item.available_from` | Aktivierungszeitpunkt |
| `${sla_response}` | `contract_sla.response_time` | Vereinbarte Reaktionszeit |

---

## Datenschnittstellen (Message Flows)

| Message | Sender-Pool | Empfänger-Pool | Protokoll | Payload-Typ | Retry-Logik |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `Service-Erstellungsauftrag` | API Gateway | CMDB | AMB/WebSocket | JSON | 3 Versuche, 30s Intervall |
| `Katalog-Registrierungsauftrag` | CMDB | Service Catalog | AMB/WebSocket | JSON | 3 Versuche, 30s Intervall |
| `Benachrichtigungsauftrag` | Service Catalog | Notification Service | AMB/WebSocket | JSON | 3 Versuche, 30s Intervall |

---

## Key Performance Indicators (KPIs)

### 1. Prozess-KPIs (Ebene Gesamtprozess)

| KPI-ID | Kennzahl | Beschreibung | Zielwert | Messmethode |
| :--- | :--- | :--- | :--- | :--- |
| **P-KPI-01** | **End-to-End-Durchlaufzeit** | Gesamtdauer vom Empfang der REST-Anfrage bis zur versendeten Benachrichtigungs-E-Mail (automatisierter Pfad ohne Approval-Wartezeit) | < 30 Sekunden | `sys_email.sys_created_on` − `sys_log.sys_created_on` (API-Request-Timestamp) |
| **P-KPI-02** | **Gesamtdurchlaufzeit inkl. Approval** | Gesamtdauer vom Empfang der REST-Anfrage bis zur versendeten Benachrichtigungs-E-Mail inkl. manuellem Approval-Schritt | < 2 Arbeitstage | `sys_email.sys_created_on` − API-Request-Timestamp |
| **P-KPI-03** | **Prozesserfolgsrate** | Anteil erfolgreich abgeschlossener Service-Anlagen ohne Fehlerfall oder manuelle Korrektur | > 98 % | Anzahl(Status=`completed`) / Gesamtanzahl Prozessinstanzen |
| **P-KPI-04** | **API-Fehlerrate** | Anteil der eingehenden API-Anfragen, die mit HTTP 4xx oder 5xx abgewiesen werden | < 2 % | Anzahl(HTTP 4xx/5xx) / Gesamtanzahl API-Calls |
| **P-KPI-05** | **CMDB-Datenqualitätsrate** | Anteil der angelegten Service-CIs, die alle Pflicht- und empfohlenen Felder vollständig befüllt haben | > 95 % | Anzahl(vollständige Datensätze) / Gesamtanzahl angelegte CIs |

### 2. Aktivitäts-KPIs (Ebene Prozessschritte)

| Aktivität(en) | KPI-Name | Beschreibung & Relevanz | Zielwert |
| :--- | :--- | :--- | :--- |
| **Serviceanfrage empfangen** (API Gateway) → **Eingabedaten validieren** (API Gateway) | **Time-to-Validation** | Dauer zwischen Empfang des HTTP-Requests und Abschluss der Schemavalidierung. Relevant als Engpass bei hohem API-Durchsatz. | < 500 ms |
| **Eingabedaten validieren** (API Gateway) → **CMDB-Erstellung auslösen** (API Gateway) | **API-Gateway-Verarbeitungszeit** | Gesamtdauer der API-Gateway-Verarbeitungskette (Validation + Kategorie-Lookup + AMB-Dispatch). Indikator für Gateway-Performance. | < 2 Sekunden |
| **CMDB-Erstellung auslösen** (API Gateway) → **Service-Stammdaten anlegen** (CMDB) | **AMB-Latenz (API→CMDB)** | Zeitdifferenz zwischen AMB-Publish und AMB-Consume durch den CMDB-Processor. Indikator für Nachrichtenbus-Auslastung. | < 1 Sekunde |
| **Service-Stammdaten anlegen** (CMDB) → **Service-Datensatz speichern** (CMDB) | **CMDB-Commit-Zeit** | Dauer der CMDB-Transaktionskette (Anlage + Attribute + Relationships + Commit). Relevant für DB-Performance. | < 5 Sekunden |
| **Katalog-Eintrag auslösen** (CMDB) → **Katalogeintrag erstellen** (Service Catalog) | **AMB-Latenz (CMDB→Catalog)** | Zeitdifferenz zwischen AMB-Publish und AMB-Consume durch den Service Catalog Processor. | < 1 Sekunde |
| **Approval-Workflow starten** (Service Catalog) → **Genehmigung verarbeiten** (Service Catalog) | **Approval-Wartezeit** | Dauer zwischen Erstellung des Approval-Tasks und Eingang der Genehmigungsentscheidung durch den Service Owner. Kritischer Wartezeittreiber im Prozess. | < 1 Arbeitstag |
| **Service aktivieren** (Service Catalog) → **Benachrichtigung auslösen** (Service Catalog) | **Time-to-Activation** | Dauer zwischen Genehmigungseingang und vollständiger Service-Aktivierung im Portal. | < 10 Sekunden |
| **Benachrichtigungsinhalt generieren** (Notification Service) → **E-Mail versenden** (Notification Service) | **Notification-Latenz** | Dauer zwischen Template-Rendering und erfolgreichem SMTP-Versand. Indikator für E-Mail-Infrastruktur-Performance. | < 30 Sekunden |

---

## Eingesetzte IT-Systeme

| System | Rolle im Prozess | Relevante Tabellen/Komponenten |
| :--- | :--- | :--- |
| **ServiceNow REST API / API Gateway** | Empfang und Vorverarbeitung eingehender Service-Anlage-Anfragen; Eingabevalidierung; AMB-Dispatch | `sys_log`, `sys_dictionary` |
| **ServiceNow CMDB** | Anlage und Pflege des Configuration Items (CI) in der zentralen Konfigurationsdatenbank; Relationship-Management | `cmdb_ci_service`, `cmdb_rel_ci`, `sys_audit` |
| **ServiceNow Service Catalog** | Erstellung des buchbaren Katalogeintrags; SLA-Zuweisung; Approval-Workflow-Steuerung; Portal-Publikation | `sc_cat_item`, `contract_sla`, `sysapproval_approver` |
| **ServiceNow Notification Service** | Empfängerermittlung; Template-basierte E-Mail-Generierung; SMTP-Versand | `sys_user`, `sys_user_grmember`, `sysevent_email_action`, `sys_email` |
| **ServiceNow AMB (Asynchronous Message Bus)** | Lose Kopplung der Subsysteme; asynchrone Nachrichtenübermittlung zwischen Pools über WebSocket | AMB-Channels (intern) |
| **ServiceNow Flow Designer** | Steuerung des Approval-Workflows (`sn_approval_workflow_service`) | Flow Designer Flows, Subflows |
| **SMTP-Relay-Server** | Ausgehender E-Mail-Versand (TLS-verschlüsselt) an interne/externe Empfänger | – |
| **Elasticsearch** | Volltext-Indexierung neu angelegter CMDB-Datensätze für die ServiceNow-Suche | – (integriert) |

---

## Sicherheitsanforderungen

| Anforderung | Maßnahme |
| :--- | :--- |
| **Authentifizierung** | Alle API-Calls erfordern gültige OAuth 2.0 Bearer Tokens oder Service-Account-Credentials |
| **Autorisierung** | ServiceNow ACLs beschränken Schreibzugriffe auf `cmdb_ci_service` und `sc_cat_item` auf autorisierte Rollen (`itil_admin`, `catalog_admin`) |
| **Transportverschlüsselung** | TLS 1.2+ für alle externen API-Calls; TLS für SMTP-Versand |
| **Eingabevalidierung** | Strikte Schema-Validierung gegen ServiceNow Table Dictionary; keine direkte SQL-Ausführung (ORM-Layer) |
| **Audit-Trail** | Alle Datenbankoperationen werden in `sys_audit` protokolliert (Wer, Was, Wann) |
| **Approval-Pflicht** | Kein Service wird ohne valide Approval-Entscheidung aktiviert (technisch erzwungen durch Workflow-Status) |

---

## Fehlerszenarien & Fallback-Strategien

| Fehlerszenario | Betroffener Pool | Auswirkung | Fallback |
| :--- | :--- | :--- | :--- |
| Validierungsfehler (Pflichtfeld fehlt) | API Gateway | Prozess bricht ab | HTTP 400 an aufrufendes System; keine CMDB-Anlage |
| Unbekannte Service-Kategorie | API Gateway | Prozess bricht ab | HTTP 422; aufrufendes System muss Kategorie korrigieren |
| AMB-Verbindungsausfall | Alle Übergänge | Nachricht geht verloren | Retry-Mechanismus (3×, 30s); Fallback auf Dead Letter Queue |
| Datenbankfehler beim CMDB-Commit | CMDB | Inkonsistenter Zustand möglich | Rollback der Transaktion; Fehlermeldung an AMB; manuelle Eskalation |
| Approval abgelehnt | Service Catalog | Service wird nicht aktiviert | `sc_cat_item.active = false`; Benachrichtigung an Requester; Prozess endet ohne Publikation |
| SMTP-Fehler | Notification Service | E-Mail nicht zugestellt | Retry (3×); Eintrag in `sys_email` mit Status `failed`; manuelle Nachbearbeitung |

---

## Referenzdokumente

- **BPMN-Modell:** `CreateBPMN/IT_Datenverarbeitung_Service_in_ServiceNow_anlegen.bpmn`
- **ServiceNow REST API Dokumentation:** [ServiceNow Table API](https://developer.servicenow.com/dev.do#!/reference/api/tokyo/rest/c_TableAPI)
- **ServiceNow CMDB Datenmodell:** ServiceNow Docs – `cmdb_ci_service` Table Reference
- **ITIL 4 Service Management Practices:** Service Configuration Management, Service Catalog Management
- **ServiceNow Flow Designer:** ServiceNow Docs – Approval Workflow Reference
- **Steckbrief-Template:** `Steckbrief_Template.md`
