# Prozesssteckbrief: Schnellball bauen

## Zusammenfassung
Der Prozess **"Schnellball bauen"** beschreibt die standardisierte Herstellung eines Schnellballs vom Auftragseingang bis zur qualitätsgesicherten Übergabe. Der Prozess beginnt mit dem Eingang eines Kundenauftrags, führt über Materialbereitstellung, Werkzeugvorbereitung, präzise Pressparameter-Einstellung (Presskraft: 250 kN ±5%), Pressung, Konditionierung und Qualitätsprüfung zur Erstellung eines fehlerfreien Messprotokolls und endet mit der Freigabe und Übergabe des geprüften Schnellballs. Ziel ist eine reproduzierbare, qualitätsgesicherte Fertigung unter Einhaltung der technischen Spezifikationen, um vorzeitiges Zerbrechen zu vermeiden und fehlerfreie Messprotokolle zu gewährleisten.

## Stammdaten
| Attribut | Wert |
| :--- | :--- |
| **Prozessname** | Schnellball bauen |
| **Prozesskategorie** | Produktion & Qualitätssicherung |
| **Auslöser** | Auftrag zum Schnellballbau eingegangen |
| **Ergebnis** | Schnellball freigegeben und übergeben |
| **Hauptverantwortung** | Organisation (Fertigungsleitung) |
| **Beteiligte Rollen** | Kunde, Organisation (Material-/Werkzeugvorbereitung, Pressbediener, QS-Messtechniker, Freigabeberechtigter, Logistik) |

## Prozessziele
1. **Produktqualität:** Sicherstellung fehlerfreier Schnellballproduktion durch exakte Einhaltung der Pressparameter (Presskraft 250 kN ±5%) und systematische Qualitätsprüfung zur Vermeidung vorzeitigen Zerbrechens.
2. **Prozessstabilität:** Gewährleistung reproduzierbarer Fertigungsergebnisse durch standardisierte Werkzeugvorbereitung, automatische Parametereinstellung und lückenlose Dokumentation im Messprotokoll.
3. **Durchlaufzeit-Effizienz:** Minimierung der Gesamtdurchlaufzeit durch optimierte Materialbereitstellung, effiziente Rüstvorgänge und parallele Konditionierungs-/Prüfphasen.
4. **Dokumentationsqualität:** Erstellung fehlerfreier Messprotokolle für jeden Schnellball zur vollständigen Rückverfolgbarkeit und Qualitätsnachweis.

## Key Performance Indicators (KPIs)

Die folgenden Kennzahlen dienen der Messung der Prozessleistung und werden in Prozess-KPIs (Gesamtbetrachtung) und Aktivitäts-KPIs (Schrittbetrachtung) unterteilt.

### 1. Prozess-KPIs (Ebene Gesamtprozess)

Diese KPIs messen den Erfolg des gesamten End-to-End-Prozesses.

| KPI-ID | Kennzahl | Beschreibung | Zielwert | Messmethode |
| :--- | :--- | :--- | :--- | :--- |
| **P-KPI-01** | **Gesamt-Durchlaufzeit** | Gesamtzeitdauer vom Auftragseingang bis zur Übergabe des freigegebenen Schnellballs inkl. Messprotokoll | < 4 Stunden | Timestamp(Übergabe) - Timestamp(Auftragseingang) |
| **P-KPI-02** | **First-Pass-Yield** | Anteil der Schnellbälle, die ohne Nacharbeit/Ausschuss die Qualitätsprüfung bestehen | > 98% | Anzahl(i.O.-Freigabe) / Anzahl(gesamt produziert) |
| **P-KPI-03** | **Messprotokoll-Fehlerrate** | Anteil der Messprotokolle ohne Auswertungsfehler oder fehlende Messwerte | < 1% | Anzahl(fehlerhafte Protokolle) / Anzahl(gesamt erstellt) × 100% |
| **P-KPI-04** | **Presskraft-Compliance** | Anteil der Pressvorgänge innerhalb der Sollvorgabe (250 kN ±5%) | > 99,5% | Anzahl(Presskraft 237,5-262,5 kN) / Anzahl(gesamt) |

### 2. Aktivitäts-KPIs (Ebene Prozessschritte)

Diese KPIs sind spezifischen Aktivitäten oder Phasen im BPMN-Modell zugeordnet, um Engpässe zu identifizieren.

| Zugeordnete Aktivität(en) | KPI-Name | Beschreibung & Relevanz | Zielwert |
| :--- | :--- | :--- | :--- |
| **Auftrag annehmen** (Organisation) → **Material bereitstellen** (Organisation) | **Time-to-Material** | Zeitdauer bis zur vollständigen Materialbereitstellung. Kritisch für Produktionsstart und Gesamtdurchlaufzeit. | < 30 Minuten |
| **Werkzeug und Presse vorbereiten** → **Pressparameter einstellen** | **Rüstzeit** | Zeitdauer für Werkzeugwechsel und Parametereinstellung. Engpass bei häufigen Produktwechseln. | < 20 Minuten |
| **Pressparameter einstellen** (Organisation) | **Parametrier-Genauigkeit** | Abweichung der eingestellten Presskraft vom Sollwert (250 kN). Direkte Auswirkung auf Produktqualität und Bruchrisiko. | ±0,5 kN (±0,2%) |
| **Schnellball pressen** (Organisation) | **Presszeit pro Einheit** | Reine Presszeit pro Schnellball. Taktgebend für Produktionskapazität. | < 2 Minuten |
| **Entformen und konditionieren** → **Mass und Funktion prüfen** | **Konditionierzeit** | Zeitdauer bis zur Prüfbereitschaft nach Entformung. Wartezeit zwischen Produktion und QS. | < 45 Minuten |
| **Mass und Funktion prüfen** (Organisation) | **Prüfzeit** | Zeitdauer für die vollständige Qualitätsprüfung inkl. Mess- und Funktionsprüfung. Kritisch für Durchlaufzeit. | < 15 Minuten |
| **Messprotokoll erstellen** (Organisation) | **Protokoll-Erstellungszeit** | Zeitdauer von Messabschluss bis zur Verfügbarkeit des validierten Messprotokolls. Automatisierungspotenzial. | < 5 Minuten |
| **Freigabe erteilen** → **Bereitstellung/Versand veranlassen** | **Time-to-Delivery** | Zeitdauer von Freigabe bis zur tatsächlichen Übergabe an den Kunden. Servicequalitäts-Indikator. | < 30 Minuten |

## Eingesetzte IT-Systeme
- **Produktionsplanungssystem (PPS):** Auftragsannahme, Materialbedarfsermittlung und Terminplanung für die Schnellball-Fertigung
- **Maschinensteuerung/SPS:** Automatische Einstellung der Pressparameter (inkl. Presskraft-Sollwert) und Überwachung der Ist-Werte während des Pressvorgangs
- **Messdatenerfassungssystem:** Automatisierte Erfassung von Prüfdaten (Abmessungen, Funktionsprüfung) und Erstellung digitaler Messprotokolle
- **Qualitätsmanagementsystem (QMS):** Dokumentation der Freigabeentscheidungen, Archivierung der Messprotokolle und Verwaltung der Prüfpläne
- **Lagerverwaltungssystem (LVS):** Verwaltung von Rohmaterial und fertigen Schnellbällen sowie Steuerung der Versandlogistik

## Referenzdokumente
- BPMN-Modell: `Schnellball_bauen.bpmn`
- Technische Spezifikation: Schnellball-Anforderungsprofil (inkl. Presskraft-Sollwerte)
- Prüfplan: QS-Prüfanweisung Schnellball (Mess- und Funktionsprüfung)
- Arbeitsanweisung: Presse einrichten und bedienen
- Arbeitsanweisung: Messprotokoll erstellen und validieren
- Freigaberichtlinie: Produktfreigabe Schnellball

---

**Erstellt am:** 26.01.2026  
**Prozessverantwortlich:** Organisation/Fertigungsleitung  
**Version:** 1.0
