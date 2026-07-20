---
Prozesseigner:
Prozessmanager:
KGSt_Produkthauptbereich: 1 Zentrale Verwaltung
KGSt_Produktbereich: 11 Innere Verwaltung
KGSt_Produktgruppe: 111 Verwaltungssteuerung und -service
KGSt_Produkt: 111.06 Informationstechnik
KGSt-Leistung:
KGSt_Prozess:
LHS_Produkt:
LHS_Aufgabe:
Name2: Technical Deployment Management
Cluster1: Run
---
# Prozess-Steckbrief: HW & SW Deployment Management

**Bezug zu IT-Strategie /Auftrag**

- Sicherstellung standardisierter, sicherer IT-Arbeitsumgebungen gemäß IT-Strategie
- Unterstützung der IT-Serviceorientierung durch zuverlässige Bereitstellung
- Grundlage für Skalierbarkeit und Wirtschaftlichkeit der IT-Infrastruktur

**Prozesszweck** Planung, Bereitstellung und Verteilung von Hard- und Softwarekomponenten in die produktive IT-Umgebung.

**Prozessziele, KPI, Werte**

- Deployment-Erfolgsquote
- Durchlaufzeit je Deployment
- Anzahl deploymentbedingter Incidents
- Standardisierungsgrad der Ausrollung

**Prozess Inputs durch Lieferanten**

- Freigegebene Releases → IT Release Management
- Zielkonfigurationen → Configuration Mgt
- Genehmigte Changes → Change Mgt
- Assets/Lizenzen → Asset Management
- Deployment-Pakete → Application Development

**Prozessaktivitäten**

- Deployment planen
- Pakete bereitstellen
- Zielsysteme konfigurieren
- Rollout durchführen
- Deployment verifizieren

**Prozess Outputs an Kunde**

- Deployte Systeme → IT Betrieb
- Deployment-Reports → Change Mgt
- Aktualisierte CI-Daten → Configuration Mgt
- Rollback-Information → Problem Mgt
- Abnahmebestätigung → Fachbereich

**Kritische Erfolgsfaktoren**

- Stabile Testumgebungen
- Klare Rollback-Strategie
- Automatisierte Deployment-Pipelines
- Enge Abstimmung mit Change Mgt

**Prozess Beteiligte / Rollen**

- Deployment Manager
- Change Manager
- IT Operations
- Configuration Manager

**Unterstützende IT-Systeme**

- Deployment-Tool (z.B. Ansible/SCCM)
- ITSM-Tool
- CMDB
