# Prozesssteckbrief: TP2 Markt sichten

## Zusammenfassung
Der Prozess **„TP2 Markt sichten"** bildet die operative Marktbeobachtungsphase innerhalb des übergeordneten Prozesses „Medienbestand managen" der Stadtbibliothek Stuttgart. Er beginnt mit dem Eingang von Leser:innenwünschen und Marktimpulsen und führt über eine systematische Sichtung aller relevanten Marktquellen, Priorisierung, Bestellinformationsanreicherung, inhaltliche Erschließung und Ressourcenprüfung zur Kaufempfehlung für die Stadtbibliothek und ihre Zweigstellen. Der Prozess endet mit einer getroffenen Kaufentscheidung als verbindlichem Input für TP3 (Medien erwerben). Ziel ist eine qualitätsgesicherte, markt- und bedarfsorientierte Erwerbungsentscheidung durch das Lektoratsteam.

## Stammdaten
| Attribut | Wert |
| :--- | :--- |
| **Prozessname** | TP2 Markt sichten |
| **Übergeordneter Prozess** | Medienbestand managen – Stadtbibliothek Stuttgart |
| **Prozesskategorie** | Bibliotheksmanagement / Medienbestandsmanagement |
| **Auslöser** | Leser:innenwünsche und Marktimpulse eingegangen |
| **Ergebnis** | Kaufentscheidung getroffen und Medienbestellung eingeleitet |
| **Hauptverantwortung** | Lektoratsteam |
| **Beteiligte Rollen** | Lektoratsteam, Bibliotheksnutzer (Kunde) |
| **Supplier** | TP01 Umfeldanalyse durchführen (Bestandsprofil) |
| **Vorgelagerter Prozess** | TP1 Umfeldanalyse durchführen |
| **Nachgelagerter Prozess** | TP3 Medien erwerben |
| **BPMN-Modell** | Bibliothek_Medienbestand_TP2_Markt_sichten.bpmn |

## Prozessziele
1. **Marktüberblick:** Vollständige und systematische Sichtung aller relevanten Marktquellen für eine informierte Erwerbungsentscheidung.
2. **Bedarfsorientierung:** Konsequente Einbeziehung von Leser:innenwünschen und Nutzer:innen-Rückmeldungen in die Priorisierung.
3. **Qualitätssicherung:** Inhaltliche Erschließung und Ressourcenprüfung als Grundlage einer fundierten Kaufempfehlung.
4. **Effizienz:** Minimierung der Durchlaufzeit von der Marktimpulssichtung bis zur Kaufentscheidung durch strukturierte Bearbeitung.
5. **Konsistenz:** Ausrichtung der Kaufempfehlung an den Bestandsprofilen aus TP1 und den spezifischen Bedarfen der Stadtteilbibliotheken.

## Detaillierte Prozessschritte

### Pool: Kunde (Bibliotheksnutzer / Bürger)

| Nr. | Schritt | Beschreibung |
| :--- | :--- | :--- |
| K1 | **Medien- und Lesewunsch mitteilen** | Der Bürger gibt einen konkreten Medienwunsch oder Anschaffungsvorschlag ab — persönlich am Auskunftsdienst, über den OPAC (aDIS/WebOPAC) oder digitale Kanäle. Dieser Wunsch fließt als Bedarfssignal in den Erwerbungsprozess ein. |

### Pool: Organisation

| Nr. | Rolle/Lane | Schritt | Beschreibung |
| :--- | :--- | :--- | :--- |
| O1 | Lektoratsteam | **Marktquellen und Input sichten** | Das Lektoratsteam sichtet systematisch alle relevanten Marktquellen: Buchbesprechungen und Rezensionen, Verlagsprogramme, Fachzeitschriften und Newsletter, Rundfunk- und TV-Beiträge, Tagespresse und Börsenblatt, Foren und Social Media, Buchmessen, Veranstaltungen, Nutzungsstatistiken, Kooperationsnetzwerke, Eigenrecherche sowie eingehende Nutzer:innen-Rückmeldungen. |
| O2 | Lektoratsteam | **Liste anlegen und priorisieren** | Auf Basis der Marktsichtung legt das Lektoratsteam eine strukturierte Medienliste an. Die identifizierten Titel werden nach Relevanz, Aktualität, Bestandskompatibilität und Nachfragepotenzial priorisiert. Das Bestandsprofil aus TP1 dient als Bewertungsrahmen. |
| O3 | Lektoratsteam | **Bestellinformationen auffüllen** | Die priorisierten Titel werden mit vollständigen Bestellinformationen angereichert: ISBN, Verlag, Erscheinungsjahr, Preis, Medienformat, Medientyp sowie Standortempfehlung (Zentrale oder Zweigstelle). |
| O4 | Lektoratsteam | **Inhaltliche Erschließung durchführen** | Das Lektoratsteam nimmt eine inhaltliche Erschließung der vorgemerkten Titel vor: Sachgruppen-Zuordnung, Schlagwortvergabe und Einordnung in die Systematik der Stadtbibliothek Stuttgart als vorbereitende Katalogisierungsarbeit für TP4. |
| O5 | Lektoratsteam | **Ressourcenprüfung durchführen** | Das Lektoratsteam prüft die Ressourcenverfügbarkeit: Budget, Regalkapazität, Mehrfachexemplarbedarf und Kompatibilität mit laufenden Abonnements. Die Prüfung stellt Realisierbarkeit im Rahmen der Ressourcenplanung aus TP1 sicher. |
| O6 | Lektoratsteam | **Kaufempfehlung für Stadtteilbibliotheken aussprechen** | Das Lektoratsteam spricht eine differenzierte Kaufempfehlung aus: Welche Titel werden zentral und welche für einzelne oder alle Stadtteilbibliotheken angeschafft? Die Kaufentscheidung ist damit getroffen und bildet den Input für TP3. |

## Key Performance Indicators (KPIs)

### 1. Prozess-KPIs (Ebene Gesamtprozess)

| KPI-ID | Kennzahl | Beschreibung | Zielwert | Messmethode |
| :--- | :--- | :--- | :--- | :--- |
| **P-KPI-01** | **Time-to-Decision (Durchlaufzeit)** | Gesamtdauer von der Marktimpulssichtung bis zur getroffenen Kaufentscheidung. | < 3 Wochen | Timestamp(Kaufentscheidung) – Timestamp(Sichtungsbeginn) |
| **P-KPI-02** | **Marktquellen-Abdeckungsrate** | Anteil der laut Prozessbeschreibung vorgesehenen Marktquellen, die je Sichtungszyklus aktiv geprüft wurden. | > 90 % | Anzahl(geprüfte Quellen) / Anzahl(definierte Quellen) |
| **P-KPI-03** | **Ressourcenkonformitätsrate** | Anteil der Kaufempfehlungen, die innerhalb des verfügbaren Budgets und der Regalkapazität liegen. | > 98 % | Anzahl(ressourcenkonforme Empfehlungen) / Gesamtanzahl(Empfehlungen) |
| **P-KPI-04** | **Leser:innenwunsch-Berücksichtigungsquote** | Anteil eingegangener Leser:innenwünsche, die in der Priorisierungsliste berücksichtigt wurden. | > 70 % | Anzahl(berücksichtigte Wünsche) / Anzahl(eingegangene Wünsche) |

### 2. Aktivitäts-KPIs (Ebene Prozessschritte)

| Zugeordnete Aktivität(en) | KPI-Name | Beschreibung & Relevanz | Zielwert |
| :--- | :--- | :--- | :--- |
| **O1 Marktquellen sichten** | **Sichtungsdauer** | Zeit für die vollständige Sichtung aller Marktquellen je Sichtungszyklus. Relevanz: Engpass durch Quellenvielfalt identifizierbar. | < 5 Werktage |
| **O1 Marktquellen sichten** → **O2 Liste anlegen** | **Titelübernahmequote** | Anteil der gesichteten Titel, die in die priorisierte Bestellliste aufgenommen werden. Relevanz: Effizienz des Sichtungsprozesses. | 10 – 25 % |
| **O2 Liste anlegen** → **O3 Bestellinfos auffüllen** | **Bestellinformations-Vollständigkeitsrate** | Anteil der Listeneinträge mit vollständig ausgefüllten Bestellinformationen beim Übergang zu O3. Relevanz: Vermeidung von Rückfragen in TP3. | > 99 % |
| **O4 Inhaltliche Erschließung** | **Erschließungszeit je Titel** | Durchschnittliche Bearbeitungszeit pro Titel für die vorbereitende inhaltliche Erschließung. Relevanz: Ressourcenplanung Lektoratsteam. | < 10 Minuten/Titel |
| **O5 Ressourcenprüfung** → **O6 Kaufempfehlung** | **Ablehnungsquote nach Ressourcenprüfung** | Anteil der Titel, die nach Ressourcenprüfung aus der Empfehlungsliste gestrichen werden. Relevanz: Qualität der Vorab-Priorisierung. | < 5 % |
| **O6 Kaufempfehlung** → **TP3 Medien erwerben** | **Übergabedauer an TP3** | Zeit zwischen Aussprechen der Kaufempfehlung und Beginn des Erwerbungsprozesses in TP3. | < 3 Werktage |

## Eingesetzte IT-Systeme
- **aDIS/BMS (aStec) – Modul Erwerbung:** Bereitstellung von Nutzungsstatistiken und Ausleihzahlen als empirische Grundlage für die Priorisierung.
- **aDIS/WebOPAC:** Entgegennahme von Leser:innenwünschen und Anschaffungsvorschlägen über den OPAC.
- **Externe Marktquellen (analog/digital):** Börsenblatt, Verlagskataloge, Fachzeitschriften, Social-Media-Plattformen, Buchmessenkataloge.

## Referenzdokumente
- BPMN-Modell: `CreateBPMN/Bibliothek_Medienbestand_TP2_Markt_sichten.bpmn`
- Bestandsprofile Literatur (Datei: `Bestandsprofile_Literatur_ausführlich.xlsx`)
- Steckbrief TP1: `CreateSteckbrief/Prozesssteckbrief_Bibliothek_TP1_Umfeldanalyse_durchfuehren.md`
