# Prozesssteckbrief: Antragstellung auf finanzielle Foerderung im Rahmen der Stuttgarter Sportfoerderung

## Zusammenfassung
Der Prozess **"Antragstellung auf finanzielle Foerderung im Rahmen der Stuttgarter Sportfoerderung"** regelt das Verfahren zur Beantragung und Bewilligung von Foerdermitteln fuer Stuttgarter Sportvereine. Er beginnt mit der Feststellung eines Foerderbedarfs durch den Antragsteller, fuehrt ueber die digitale Einreichung, die automatisierte Vorpruefung durch das IT-System und die fachliche Pruefung sowie Entscheidung durch die zust&auml;ndige Behoerde und endet mit der digitalen Zustellung des Foerderbescheids. Ziel ist eine effiziente, transparente und rechtssichere Bearbeitung von Sportfoerderantraegen unter Nutzung digitaler Verwaltungsleistungen und unter Einbindung aller beteiligten Stellen.

## Stammdaten
| Attribut | Wert |
| :--- | :--- |
| **Prozessname** | Antragstellung auf finanzielle Foerderung – Stuttgarter Sportfoerderung |
| **Prozesskategorie** | Buerger-Service / Sportfoerderung / Subventionsverwaltung |
| **Ausloser** | Foerderbedarf festgestellt |
| **Ergebnis** | Foerderbescheid zugestellt |
| **Hauptverantwortung** | Amt fuer Sport und Bewegung / Behoerde Sportfoerderung |
| **Beteiligte Rollen** | Buerger (Antragsteller / Sportverein), IT (digitale Annahme und Vorpruefung), Behoerde (Sachbearbeitung und Bescheiderstellung) |

## Prozessziele
1. **Effizienz:** Beschleunigung der Antragsbearbeitung durch digitale Einreichung, automatisierte IT-Vorpruefung und strukturierte Weitergabe der Antragsdaten an die Behoerde.
2. **Qualitaet:** Sicherstellung vollstaendiger und fehlerfreier Antragsdaten durch IT-gestutzte Vorpruefung der Unterlagen vor Weiterleitung an die Sachbearbeitung.
3. **Rechtssicherheit:** Einhaltung der foerderrechtlichen Grundlagen der Stuttgarter Sportfoerderrichtlinien bei der Pruefung der Foerderfaehigkeit und der Festlegung des Foerderbetrags.
4. **Serviceorientierung:** Vereinfachte und medienbruchfreie Antragstellung fuer Sportvereine sowie transparente digitale Zustellung des Foerderbescheids.
5. **Transparenz:** Nachvollziehbare Dokumentation des Bearbeitungsstatus durch definierte Uebergabepunkte zwischen Buerger, IT und Behoerde.

## Key Performance Indicators (KPIs)

Die folgenden Kennzahlen dienen der Messung der Prozessleistung und werden in Prozess-KPIs (Gesamtbetrachtung) und Aktivitaets-KPIs (Schrittbetrachtung) unterteilt.

### 1. Prozess-KPIs (Ebene Gesamtprozess)

Diese KPIs messen den Erfolg des gesamten End-to-End-Prozesses.

| KPI-ID | Kennzahl | Beschreibung | Zielwert | Messmethode |
| :--- | :--- | :--- | :--- | :--- |
| **P-KPI-01** | **Durchlaufzeit (End-to-End)** | Gesamtdauer vom digitalen Antragseingang beim IT-System bis zur Zustellung des Foerderbescheids beim Antragsteller. | < 30 Arbeitstage | Timestamp(Bescheid zugestellt) - Timestamp(Antrag eingegangen) |
| **P-KPI-02** | **First-Pass-Yield (FPY)** | Anteil der Antraege, die ohne Rueckfragen oder Nachforderungen vollstaendig bearbeitet werden koennen. | > 80% | Anzahl(Antraege ohne Nachforderung) / Gesamtanzahl(Antraege) |
| **P-KPI-03** | **Termintreue** | Einhaltung der intern vorgegebenen Bearbeitungsfristen gemaess Sportfoerderrichtlinien. | > 90% | Anzahl(fristgerechte Bearbeitungen) / Gesamtanzahl(Bearbeitungen) |
| **P-KPI-04** | **Digitalisierungsgrad** | Anteil der Antraege, die vollstaendig digital (ohne Medienbruch) eingereicht und bearbeitet werden. | > 95% | Anzahl(volldigitale Antraege) / Gesamtanzahl(Antraege) |

### 2. Aktivitaets-KPIs (Ebene Prozessschritte)

Diese KPIs sind spezifischen Aktivitaeten oder Phasen im BPMN-Modell zugeordnet, um Engpaesse zu identifizieren.

| Zugeordnete Aktivitaet(en) | KPI-Name | Beschreibung & Relevanz | Zielwert |
| :--- | :--- | :--- | :--- |
| **Antrag vorbereiten** (Buerger) → **Antrag einreichen** (Buerger) | **Vorbereitungsdauer** | Zeitspanne zwischen Start des Antragsformulars und vollstaendiger Einreichung. Indikator fuer Verstaendlichkeit und Nutzerfreundlichkeit des Formulars. | < 1 Arbeitstag |
| **Antrag erfassen** (IT) → **Unterlagen pruefen** (IT) | **Systemseitige Erfassungszeit** | Zeitdauer der automatisierten Erfassung und Strukturierung der Antragsdaten im IT-System. Engpassindikator fuer die technische Eingangsverarbeitung. | < 2 Stunden |
| **Unterlagen pruefen** (IT) → **Antragsdaten uebermitteln** (IT) | **IT-Vorpruefungszeit** | Dauer der automatisierten Vollstaendigkeitspruefung der eingereichten Unterlagen. Kritisch fuer fruehzeitige Fehlererkennung vor der fachlichen Pruefung. | < 4 Stunden |
| **Antragsdaten uebermitteln** (IT) → **Zustaendigkeit pruefen** (Behoerde) | **Uebergabezeit IT zu Behoerde** | Liegezeit zwischen Datenuebermittlung durch das IT-System und Beginn der fachlichen Bearbeitung durch die Behoerde. Wartezeit-Indikator an der Schnittstelle IT/Behoerde. | < 1 Arbeitstag |
| **Zustaendigkeit pruefen** (Behoerde) → **Foerderfaehigkeit bewerten** (Behoerde) | **Zustaendigkeitspruefungszeit** | Zeitbedarf fuer die formale Pruefung der sachlichen und oertlichen Zustaendigkeit. Voraussetzung fuer die inhaltliche Pruefung. | < 2 Arbeitstage |
| **Foerderfaehigkeit bewerten** (Behoerde) → **Foerderbetrag festlegen** (Behoerde) | **Foerderpruefungsdauer** | Zeitspanne fuer die inhaltliche Bewertung des Antrags anhand der Sportfoerderrichtlinien. Kernaktivitaet mit hoechstem Komplexitaetsgrad. | < 10 Arbeitstage |
| **Foerderbetrag festlegen** (Behoerde) → **Bescheid erstellen** (Behoerde) | **Bescheiderstellungszeit** | Zeitbedarf fuer die Festlegung des Foerderbetrags und die Erstellung des rechtskraeftigen Foerderbescheids. | < 2 Arbeitstage |
| **Bescheid bereitstellen** (IT) → **Bescheid empfangen** (Buerger) | **Zustellungsdauer** | Zeitspanne zwischen digitaler Bereitstellung des Bescheids durch das IT-System und Empfangsbestaetigung des Antragstellers. | < 1 Arbeitstag |

## Eingesetzte IT-Systeme
- **Stuttgarter Foerderportal / Buergerportal:** Digitale Plattform zur Einreichung des Foerderantrags durch den Antragsteller (Buerger-Pool).
- **Antragsmanagementsystem (AMS):** IT-seitiges System zur automatisierten Erfassung, Vollstaendigkeitspruefung und strukturierten Weitergabe der Antragsdaten an die Behoerde.
- **Fachverfahren Sportfoerderung:** Behoerdensystem zur fachlichen Pruefung, Foerderentscheidung und Bescheiderstellung gemaess den Stuttgarter Sportfoerderrichtlinien.
- **DMS (Dokumentenmanagementsystem):** Elektronische Aktenführung und Archivierung aller Antragsunterlagen und Bescheide.
- **Output-Management-System:** Automatisierte digitale Bereitstellung und Zustellung des Foerderbescheids an den Antragsteller.

## Referenzdokumente
- BPMN-Modell: `Stuttgarter_Sportfoerderung_beantragen.bpmn`
- Formular: `Sportfoerderung_Antrag_vorbereiten.form`
- Sportfoerderrichtlinien der Landeshauptstadt Stuttgart (jeweils aktuelle Fassung)
- Gemeindeordnung Baden-Wuerttemberg (GemO BW) – Grundlage kommunaler Foerdertatigkeit
- DSGVO sowie Landesdatenschutzgesetz Baden-Wuerttemberg (LDSG BW) – Datenschutz bei der Verarbeitung von Antragsdaten
- Interne Arbeitsanweisung Amt fuer Sport und Bewegung – Bearbeitung von Foerderantraegen
