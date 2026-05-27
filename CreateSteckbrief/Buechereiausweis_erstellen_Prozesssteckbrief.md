# Prozesssteckbrief: Buechereiausweis erstellen

## Zusammenfassung
Der Prozess **"Buechereiausweis erstellen"** dient dazu, fuer eine antragstellende Person einen gueltigen Buechereiausweis bereitzustellen, damit Bibliotheksleistungen genutzt werden koennen. Der Prozess beginnt mit dem Antrag des Buergers, fuehrt ueber die Pruefung durch die Bibliothek und die technische Erstellung im IT-System zur Ausgabe des fertigen Ausweises. Ziel ist eine schnelle, serviceorientierte und fehlerfreie Bereitstellung des Buechereiausweises.

## Stammdaten
| Attribut | Wert |
| :--- | :--- |
| **Prozessname** | Buechereiausweis erstellen |
| **Prozesskategorie** | Buergerservice, Kultur |
| **Auslöser** | Antrag auf Buechereiausweis eingegangen |
| **Ergebnis** | Buechereiausweis erstellt und ausgegeben |
| **Hauptverantwortung** | Bibliothek |
| **Beteiligte Rollen** | Buerger, IT, Bibliothek |

## Prozessziele
1. **Effizienz:** Die Bearbeitung des Antrags soll eine moeglichst kurze Durchlaufzeit haben, um den Ausweis schnell bereitzustellen.
2. **Qualitaet:** Die Datenerfassung und Ausweiserstellung sollen fehlerfrei erfolgen, um Nacharbeiten und fehlerhafte Ausweise zu vermeiden.
3. **Serviceorientierung:** Der Prozess soll fuer den Buerger einfach, transparent und mit minimalem Aufwand verbunden sein.
4. **Automatisierung:** Die technischen Schritte der Datenerfassung, Validierung und Ausweiserstellung sollen vollautomatisiert im IT-System ablaufen.

## Key Performance Indicators (KPIs)

Die folgenden Kennzahlen dienen der Messung der Prozessleistung und werden in Prozess-KPIs (Gesamtbetrachtung) und Aktivitäts-KPIs (Schrittbetrachtung) unterteilt.

### 1. Prozess-KPIs (Ebene Gesamtprozess)

Diese KPIs messen den Erfolg des gesamten End-to-End-Prozesses.

| KPI-ID | Kennzahl | Beschreibung | Zielwert | Messmethode |
| :--- | :--- | :--- | :--- | :--- |
| **P-KPI-01** | **Gesamtdurchlaufzeit** | Misst die Zeit vom Eingang des Antrags bis zur Ausgabe des Ausweises an den Buerger. | < 15 Minuten | Timestamp(Task_Ausweis_ausgeben) - Timestamp(StartEvent_Antrag_eingegangen) |
| **P-KPI-02** | **Erst-Erfolgs-Rate** | Anteil der Antraege, die ohne Korrekturschleifen oder manuelle Dateneingriffe im IT-System verarbeitet werden. | > 98% | (Anzahl fehlerfreie Antraege / Gesamtanzahl Antraege) * 100 |
| **P-KPI-03** | **Automatisierungsgrad** | Anteil der vollautomatisierten Aktivitaeten im IT-Prozess (Erfassen, Validieren, Erzeugen). | 100% | Anzahl(automatisierte Tasks) / Anzahl(gesamte IT-Tasks) |

### 2. Aktivitäts-KPIs (Ebene Prozessschritte)

Diese KPIs sind spezifischen Aktivitäten oder Phasen im BPMN-Modell zugeordnet, um Engpässe zu identifizieren.

| Zugeordnete Aktivität(en) | KPI-Name | Beschreibung & Relevanz | Zielwert |
| :--- | :--- | :--- | :--- |
| **Task_Antrag_entgegennehmen** (Bibliothek) → **Task_Berechtigung_pruefen** (Bibliothek) | **Pruefzeit Berechtigung** | Zeit, die fuer die manuelle Pruefung der Antragsberechtigung benoetigt wird. Ein Indikator fuer die manuelle Arbeitslast. | < 3 Minuten | Timestamp(Ende Pruefung) - Timestamp(Start Pruefung) |
| **Task_Registrierungsanfrage_stellen** (Bibliothek) → **Event_Ausweisdaten_erhalten** (Bibliothek) | **IT-Verarbeitungszeit** | Misst die reine Verarbeitungszeit des IT-Systems von der Anfrage bis zur Bereitstellung der fertigen Ausweisdaten. | < 30 Sekunden | Timestamp(Event_Ausweisdaten_erhalten) - Timestamp(Task_Registrierungsanfrage_stellen) |
| **Task_Personendaten_erfassen** (IT) → **Task_Ausweisdaten_bereitstellen** (IT) | **System-Durchlaufzeit** | Interne Durchlaufzeit im IT-System. Relevant zur Ueberwachung der System-Performance. | < 20 Sekunden | Timestamp(Task_Ausweisdaten_bereitstellen) - Timestamp(Task_Personendaten_erfassen) |
| **Event_Ausweisdaten_erhalten** (Bibliothek) → **Task_Ausweis_ausgeben** (Bibliothek) | **Ausgabezeit** | Zeit, die benoetigt wird, um den physischen oder digitalen Ausweis an den Buerger auszugeben. | < 2 Minuten | Timestamp(Task_Ausweis_ausgeben) - Timestamp(Event_Ausweisdaten_erhalten) |
| **Task_Antrag_absenden** (Buerger) → **StartEvent_Antrag_eingegangen** (Bibliothek) | **Uebermittlungsdauer** | Zeit fuer die technische Uebermittlung des Antrags vom Buerger-Frontend zum Bibliothekssystem. | < 5 Sekunden | Timestamp(StartEvent_Antrag_eingegangen) - Timestamp(Task_Antrag_absenden) |

## Eingesetzte IT-Systeme
- **Bibliotheks-Management-System:** Fachverfahren zur Verwaltung von Mitgliedern, Medien und Ausleihvorgaengen. Fuehrt die Erstellung und Validierung der Ausweisdaten durch.
- **Online-Antragsportal:** Web-Frontend, ueber das Buerger den Antrag digital stellen koennen.

## Referenzdokumente
- BPMN-Modell: `Buechereiausweis_erstellen.bpmn`
- Formular: `Buechereiausweis_Antrag.form`
- [Satzung der oeffentlichen Bibliothek der Stadt/Gemeinde]

---
