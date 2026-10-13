# KI-gestützte Prozessmodellierung mit GovModeler BPMN

## Pilotierung im Schulverwaltungsamt der Landeshauptstadt Stuttgart

**Dokumententyp:** PoC-Konzept  
**Projekt:** KI-gestützte BPMN-Prozessmodellierung im Rahmen des stadtweiten Geschäftsprozessmanagements (GPM)  
**Pilotbereich:** Schulverwaltungsamt der Landeshauptstadt Stuttgart  
**Ausführende Einheit:** 17-3.4  
**Werkzeug:** GovModeler mit Agent 40

---

## 1. Ausgangslage und Ziele

Im Rahmen des stadtweiten Geschäftsprozessmanagements wird die KI-gestützte Erstellung von BPMN-Prozessmodellen mit GovModeler erprobt. Der PoC im Schulverwaltungsamt dient dazu, die Praxistauglichkeit von Agent 40 für die Modellierung der vom Amt benannten Prozesse zu prüfen und den Agenten anhand der gewonnenen Erkenntnisse gezielt weiterzuentwickeln.

Das Schulverwaltungsamt benennt den zu modellierenden Prozess. Die Erstellung des BPMN-Modells erfolgt durch 17-3.4 mithilfe von Agent 40. Anschließend prüft das Schulverwaltungsamt das Modell fachlich und übernimmt es nach gegebenenfalls erforderlichen Korrekturen.

Die Ziele des PoC sind:

- Erstellung von BPMN-Modellen für die durch das Schulverwaltungsamt benannten Prozesse.
- Erprobung eines schlanken Ablaufs von der Prozessbenennung bis zur fachlichen Prüfung und Übernahme.
- Bewertung der Qualität und Nutzbarkeit der KI-generierten Modelle sowie des Erstellungs-, Prüf- und Korrekturaufwands.
- Sammlung von Rückmeldungen und Verbesserungsvorschlägen in einem Backlog für die iterative Weiterentwicklung von Agent 40.

KI-generierte Modelle sind zunächst Entwürfe. Eine fachliche Prüfung durch das Schulverwaltungsamt wird durch den KI-Einsatz nicht ersetzt.

## 2. Vorgehen

### 2.1 Prozessbenennung durch das Schulverwaltungsamt

Das Schulverwaltungsamt benennt den Prozess, der als BPMN-Modell erstellt werden soll. Die Prozessbenennung bildet den Ausgangspunkt der Modellierung. Soweit vorhanden, können ergänzende fachliche Angaben bereitgestellt werden. Fehlende Informationen werden im weiteren Verlauf gezielt geklärt.

### 2.2 Modellerstellung durch 17-3.4

17-3.4 erstellt mithilfe von Agent 40 einen BPMN-Modellentwurf. Die Erstmodellierung konzentriert sich auf den regulären Prozessablauf (Happy Path). Annahmen und offene fachliche Fragen werden begleitend dokumentiert, damit sie bei der Prüfung eindeutig erkennbar sind.

17-3.4 stellt das BPMN-Modell dem Schulverwaltungsamt in ADONIS zur Prüfung und weiteren Verwendung zur Verfügung.

### 2.3 Fachliche Prüfung durch das Schulverwaltungsamt

Das Schulverwaltungsamt prüft methodisch, ob das Modell den tatsächlichen Prozessablauf zutreffend abbildet. Im Mittelpunkt stehen Start- und Endereignis, wesentliche Prozessschritte, deren Reihenfolge sowie die dargestellten Zuständigkeiten. Annahmen und offene Fragen werden bestätigt, korrigiert oder ergänzt. Das Schulverwaltungsamt gibt 17-3.4 eine schriftliche Rückmeldung zu den methodischen Mängeln und macht Verbesserungsvorschläge.

Erforderliche inhaltliche Änderungen werden nicht an 17-3.4 zurückgemeldet, sondern von 40 selbst vorgenommen.

### 2.4 Übernahme des Prozessmodells

Nach Abschluss der fachlichen Prüfung und der erforderlichen Korrekturen übernimmt das Schulverwaltungsamt das Prozessmodell. Die Übernahme wird nachvollziehbar dokumentiert. Sie bezieht sich auf den geprüften Modellstand und den vereinbarten Modellierungsumfang.

## 3. Iterative Weiterentwicklung von Agent 40

Parallel zur Bearbeitung der Prozesse wird Agent 40 anhand eines Backlogs weiterentwickelt. Grundlage sind die Erfahrungen von 17-3.4 bei der Modellerstellung sowie die Rückmeldungen des Schulverwaltungsamts.

Der Verbesserungszyklus umfasst:

1. **Rückmeldungen erfassen:** Wiederkehrende Fehler, unpassende Fachbegriffe, fehlende Modellierungsregeln und Verbesserungsvorschläge werden im Backlog gesammelt. Korrekturen an einzelnen Modellen werden von allgemeinen Verbesserungen des Agenten unterschieden.
2. **Backlog priorisieren:** 17-3.4 priorisiert die Einträge unter Berücksichtigung der fachlichen Rückmeldungen, ihrer Auswirkungen auf die Modellqualität und des Umsetzungsaufwands.
3. **Agenten anpassen:** 17-3.4 entwickelt die Vorgaben und Anweisungen von Agent 40 schrittweise weiter.
4. **Änderungen prüfen:** Die Anpassungen werden anhand ausgewählter Beispielprozesse überprüft. Dabei wird geprüft, ob das adressierte Problem behoben wurde und bereits funktionierende Modellierungsregeln erhalten bleiben.
5. **Stand dokumentieren:** Änderungen, Prüfergebnisse und der jeweils eingesetzte Agentenstand werden nachvollziehbar festgehalten. Daraus können weitere Backlog-Einträge entstehen.

Änderungen an Agent 40 führen nicht automatisch zu Änderungen bereits übernommener Prozessmodelle. Eine erneute Modellierung oder Anpassung erfolgt bei Bedarf und erfordert eine erneute fachliche Prüfung.

## 4. Scope

### 4.1 In-Scope

- BPMN-Modellerstellung für Prozesse, die das Schulverwaltungsamt benennt.
- Einsatz von Agent 40 durch 17-3.4.
- Erstmodellierung des regulären Prozessablaufs (Happy Path).
- Methodische und fachliche Prüfung durch das Schulverwaltungsamt.
- Rückmeldung zu Mängeln und Verbesserungsvorschläge an 17-3.4.
- Prüfung der technischen Anschlussfähigkeit an ADONIS.
- Backlog-basierte, iterative Weiterentwicklung von Agent 40.

### 4.2 Out-of-Scope

- Prozesse außerhalb des Schulverwaltungsamts.
- Vollständige Modellierung aller Ausnahme- und Fehlerpfade in der KI-Erstgenerierung.
- Technische Umsetzung von Digitalisierungs- oder Automatisierungslösungen.
- Flächendeckende Einführung des Werkzeugs oder Übernahme von Modellen ohne fachliche Prüfung.

## 5. Bewertung

Der PoC wird anhand des tatsächlichen Bearbeitungsverlaufs und der Rückmeldungen des Schulverwaltungsamts bewertet. Erstellungs-, Prüf- und Korrekturaufwand werden getrennt betrachtet, damit zusätzlicher Prüfaufwand nicht als Zeitersparnis erscheint.

| Dimension | Leitfrage | Messgröße / Indikator |
| --- | --- | --- |
| **Bearbeitungsaufwand** | Welcher Aufwand entsteht von der Prozessbenennung bis zur Übernahme? | Zeit für Erstellung, fachliche Prüfung und Korrekturen je Prozess |
| **Fachliche Qualität** | Wie zutreffend bildet der Erstentwurf den tatsächlichen Ablauf ab? | Anzahl und Art fachlicher Korrekturen; ohne Änderung übernommene Schritte |
| **Übernahmefähigkeit** | Kann das Schulverwaltungsamt das Modell nach der Prüfung übernehmen? | Übernahmestatus und Anzahl der erforderlichen Korrekturschleifen |
| **Technische Anschlussfähigkeit** | Lässt sich das Modell in ADONIS übernehmen und weiterbearbeiten? | Ergebnis der Importprüfung und erforderliche technische Nacharbeit |
| **Wirksamkeit der Agentenentwicklung** | Verbessern die Backlog-Anpassungen die Modellqualität? | Ergebnisse der Prüfungen vor und nach Anpassungen; Wiederauftreten bekannter Fehler |

Eine Zeitersparnis gegenüber dem klassischen Vorgehen wird nur ausgewiesen, wenn eine nachvollziehbare Vergleichsbasis für vergleichbare Prozesse vorliegt. Andernfalls wird der beobachtete Aufwand dokumentiert, ohne einen Einsparungseffekt zu behaupten.