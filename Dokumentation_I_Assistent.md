# Aktenvermerk: Technische und fachliche Umsetzung des Agenten I

**Themenfeld:** Prozessmanagement und künstliche Intelligenz  
**Dokumentationsstand:** 09.10.2026  
**Gegenstand:** Beschreibung und BPMN-Modellierung von IT-Datenverarbeitungsprozessen durch den Custom Agent GovModeler_I in Visual Studio Code mit GitHub Copilot

## 1. Anlass und Zielsetzung

Der Agent I unterstützt im Projekt GovModeler die Beschreibung und Modellierung von Datenverarbeitungsprozessen aus Sicht der IT. Ausgehend von einem Prozessnamen soll er eine technisch ausgerichtete Ablaufbeschreibung erstellen und anschließend automatisch in ein Modell nach Business Process Model and Notation (BPMN) überführen. Im Mittelpunkt stehen der Empfang, die Prüfung, die Verarbeitung, die Speicherung und die Weitergabe von Daten.

Der Bezug zum Prozessmanagement besteht in der Darstellung technischer Aktivitäten, beteiligter IT-Systeme und ihrer Datenbeziehungen. Jedes beteiligte IT-System soll einen eigenen Pool erhalten. Der Datenaustausch zwischen den Systemen wird als Kollaboration dargestellt. Pools für Bürger, Behörden oder Fachbereiche sind in der vorgesehenen Modellstruktur nicht enthalten.

Die KI übernimmt die sprachliche Ausarbeitung der technischen Beschreibung und deren Übersetzung in eine BPMN-Struktur einschließlich Diagramminformationen. Ziel sind eine Prozessbeschreibung und eine bearbeitbare Modelldatei als Grundlage für die weitere fachliche und technische Bearbeitung. Der Agent führt die beschriebenen Verarbeitungsschritte nicht selbst aus und implementiert dadurch keine Schnittstellen oder Dienste. Dieser Vermerk beschreibt die hinterlegte Konfiguration und den vorgesehenen Bearbeitungsablauf. Eine Bewertung oder Evaluation des Agenten ist nicht Gegenstand.

## 2. Fachliche Umsetzung und Wissensbasis

Ausgangspunkt ist ein von der anfragenden Person genannter Prozessname. Die Agentenanweisung verlangt zunächst eine Zusammenfassung in zwei bis drei Sätzen zum Zweck und zu den beteiligten Akteuren. Anschließend soll eine detaillierte Beschreibung des Startereignisses, der chronologischen Verarbeitungsschritte und des Endereignisses entstehen.

Für das Startereignis sind Auslöser, Trigger-Art, Datenquelle, Datenformat und beispielhafte Eingabedaten vorgesehen. Jeder Verarbeitungsschritt soll eine Nummer, eine Bezeichnung nach dem Muster „Substantiv + Verb“ und das verarbeitende System beziehungsweise die Komponente enthalten. Hinzu kommen Angaben zu Input, Verarbeitungslogik, Output und Persistierung. Die Beschreibung soll unter anderem Validierung, Transformation, Anreicherung, Filterung und Berechnungen erläutern, soweit diese zum Prozess gehören.

Bei systemübergreifendem Austausch sollen Quell- und Zielsystem, Schnittstellenart, Protokoll und Datenflussrichtung benannt werden. Externe Dienste sowie verwendete Stamm- oder Referenzdaten sind als technische Abhängigkeiten zu beschreiben. Das Endereignis soll den erreichten Zustand, die finalen Daten und deren Nutzung durch nachfolgende Systeme oder Prozesse erläutern. Konkrete Systemnamen, relevante Datenfelder und Datentypen sowie ein förmlicher, technisch präziser Kommunikationsstil sind vorgegeben.

Die Beschreibung ist auf den regulären, erfolgreichen Ablauf beschränkt, den die Anweisung als „Happy Path“ bezeichnet. Alternativpfade, Fehlerfälle und parallele Abläufe sind nicht vorgesehen. Bei kritischen Validierungen soll erwähnt werden, dass nur valide Daten weitergeleitet werden. Dies beschreibt den erfolgreichen Verarbeitungspfad, nicht eine modellierte Fehlerbehandlung.

Die Agentenanweisung enthält unterschiedliche Angaben zur Detailtiefe: In den Grundprinzipien nennt sie wesentliche Verarbeitungsschritte und höchstens fünf bis sieben Tasks je Pool, abhängig von der Komplexität. In den späteren Modellierungsabschnitten verlangt sie hingegen einen eigenen Task für jeden technischen Verarbeitungsschritt und nennt ausdrücklich keine Obergrenze. Der Vermerk gibt diese Vorgaben als Bestandteile der Konfiguration wieder; eine einheitliche zahlenmäßige Begrenzung wird daraus nicht abgeleitet.

Die für I maßgeblichen Informationsquellen haben unterschiedliche Funktionen:

- **Agentenanweisung:** IT-Perspektive, Beschreibungstiefe, Datenflussangaben, Modellstruktur, Arbeitsschritte und Ausgabe.
- **Prozessangabe und ergänzende Informationen der anfragenden Person:** Ausgangspunkt und gegebenenfalls Konkretisierung der tatsächlichen Systeme und Datenverarbeitung.
- **BPMN-Vorlage:** technische Grundstruktur als Referenz für die Modellerstellung.
- **BPMN-DI-Richtlinien:** Vorgaben zur Diagrammdarstellung, Anordnung der Elemente und Führung der Verbindungen.
- **Projektdokumentation:** technische Voraussetzungen und Nutzung über Copilot Chat.

Vor der Modellierung müssen nach der Anweisung beide Referenzdateien tatsächlich gelesen werden. Eine verbindliche prozessspezifische Systemdokumentation, Schnittstellenspezifikation oder rechtliche Wissensquelle ist dagegen nicht als Pflichtquelle festgelegt. Die geforderten Angaben zu Systemen, Datenformaten und Verarbeitung sind daher von einer anhand technischer Unterlagen bestätigten Beschreibung des realen Betriebs zu unterscheiden.

## 3. Technische Umsetzung

I ist als Custom Agent in Visual Studio Code mit GitHub Copilot konfiguriert. Die [Agentendatei](.github/agents/GovModeler_I.agent.md) besteht aus einem YAML-Kopf mit Einsatzbeschreibung und Werkzeugauswahl sowie einem Anweisungstext. Die Einsatzbeschreibung nennt die Prozessbeschreibung im Pool IT. Der Anweisungstext konkretisiert dies als Modellierung mit separaten Pools für die beteiligten IT-Systeme, nicht als verpflichtende Beschränkung auf einen einzigen Pool.

Die Werkzeugauswahl umfasst das Erstellen und Lesen von Dateien, Suchfunktionen sowie Terminalausführung und den Zugriff auf Terminalausgaben. Damit ist die Konfiguration auf die Verarbeitung von Projektunterlagen und die Erzeugung von Modelldateien ausgerichtet. Die verfügbaren Werkzeuge und Arbeitsschritte beschreiben das vorgesehene Vorgehen; dieser Vermerk dokumentiert keinen konkreten Ausführungslauf.

Die Referenzdateien sind zuerst direkt im Wurzelverzeichnis des aktuellen Repositorys zu öffnen. Falls dies fehlschlägt, ist ausschließlich im geöffneten Workspace nach ihnen zu suchen. Ein eindeutiger Treffer soll ohne Rückfrage verwendet werden. Nur bei fehlenden Dateien oder mehreren widersprüchlichen Treffern ist ein Hinweis an die anfragende Person vorgesehen. Externe Verzeichnisse, lokale Benutzerpfade und konstruierte Pfade außerhalb des Repositorys sind ausgeschlossen. In virtuellen GitHub-Workspaces sollen die gefundenen virtuellen Dateiadressen unmittelbar verwendet werden.

Als Ausgabe ist eine XML-Datei mit der Endung `.bpmn` vorgesehen. Neben den Prozess- und Kollaborationselementen soll sie Informationen nach BPMN Diagram Interchange (BPMN-DI) enthalten. Diese beschreiben Positionen und Größen der sichtbaren Elemente sowie Wegpunkte ihrer Verbindungen. Die vorhandene BPMN-Vorlage dient als Grundstruktur; die konkrete Teilnehmerstruktur legt die I-Agentenanweisung mit einem Pool je IT-System fest.

Jeder System-Pool soll ein eigenes Start- und Endereignis enthalten. Innerhalb der Pools werden die Tasks horizontal ausgerichtet. Für die Poolbreite sind mindestens 1200 Pixel und eine dynamische Anpassung an die Taskanzahl vorgesehen. Die Pools werden vertikal gestaffelt; Koordinaten und Abstände sind in der Agentenanweisung beschrieben.

Service Tasks sind für automatische Datenverarbeitung, Script Tasks für Datenmanipulation und Send beziehungsweise Receive Tasks für systemübergreifenden Datenaustausch vorgesehen. Message Flows verbinden die IT-Pools über Sende- und Empfangsaufgaben oder zwischengeschaltete Nachrichtenereignisse. Sie erhalten sprechende Namen, die den ausgetauschten Daten entsprechen. Der Anweisung zufolge sind technische Verarbeitungsschritte wie Datenempfang, Validierung, Prüfung, Transformation, Anreicherung, Berechnung, Speicherung und Benachrichtigung einzeln zu modellieren, soweit sie zum beschriebenen Prozess gehören.

Die Datei soll im Ordner CreateBPMN unter einem prozessbezogenen Namen mit IT-Präfix gespeichert werden, beispielsweise `IT_Datenverarbeitung_Wohngeldantrag.bpmn`. Anschließend ist das automatische Öffnen in der VS-Code-Erweiterung „Camunda Modeler by miragon“ vorgesehen. Die technische Projektdokumentation nennt GitHub Copilot und Copilot Chat für die KI-Interaktion sowie den Camunda Modeler für die Darstellung und Bearbeitung der Modelle.

Die Umsetzung verbindet das Sprachmodell zur Interpretation und Generierung, die Agentenanweisung zur Steuerung und dateibasierte Referenzen zur Modellstruktur. Die Vorgaben sind natürlichsprachlich formuliert. Eine separate programmatische Durchsetzung ist in der Agentendatei nicht implementiert. Ein eigenes Training auf Projektunterlagen, eine separate Vektordatenbank oder eine eigenständig implementierte Retrieval-Pipeline sind in den herangezogenen Unterlagen nicht beschrieben.

Ein bestimmtes KI-Modell oder eine Modellversion ist in der I-Agentendatei nicht festgelegt. Die technische Dokumentation sieht die Modellauswahl in Copilot Chat vor. Hosting, Speicherung von Eingaben und betriebliche Datenschutzregelungen werden in der Agentendatei nicht beschrieben; hierzu trifft dieser Vermerk keine weitergehenden Feststellungen.

## 4. Bearbeitungsablauf und Ausgabe

Die Interaktion erfolgt über Copilot Chat. Nach Auswahl des Modells und des Agenten wird der Prozess benannt. Die I-Agentenanweisung sieht folgenden Ablauf vor:

1. **Prozessbeschreibung erstellen:** Zweck und beteiligte Systeme zusammenfassen; Startereignis, Verarbeitungsschritte, Datenbeziehungen und Endereignis technisch beschreiben.
2. **Darstellungsrahmen erläutern:** Darüber informieren, dass der Prozess aus IT-Sicht mit separaten System-Pools dargestellt wird und Datenschnittstellen als Message Flows modelliert werden.
3. **Referenzen auflösen und lesen:** Die beiden Referenzdateien im aktuellen Repository öffnen beziehungsweise dort suchen und vor der Modellierung tatsächlich lesen.
4. **BPMN-Modell automatisch erstellen:** Die Verarbeitungsschritte in Tasks und Ereignisse überführen, je IT-System einen Pool anlegen und Datenbeziehungen sowie Diagramminformationen ergänzen.
5. **Datei speichern:** Das Modell mit einem sprechenden, IT-bezogenen Dateinamen und der Endung `.bpmn` im Ordner CreateBPMN ablegen.
6. **Modell öffnen und Vorgaben prüfen:** Die Datei automatisch in der Camunda-Modeler-Erweiterung öffnen, darüber informieren und die in der Anweisung aufgeführten Abschlussprüfungen vornehmen.

Eine zusätzliche Bestätigung zwischen Prozessbeschreibung und Modellerstellung ist in der I-Agentenanweisung nicht vorgesehen. Sie verlangt nach der Beschreibung ausdrücklich die automatische Erstellung und anschließend das automatische Öffnen des Modells.

Die vorgesehenen Abschlussprüfungen betreffen unter anderem das Lesen der Referenzen, die separaten System-Pools, die Nachrichtenflüsse, die horizontale Anordnung, den Happy Path, die einzelne Darstellung der Verarbeitungsschritte, die dynamische Poolbreite sowie Speicherung, Dateiname und Öffnen im Editor. Sie sind Bestandteil des konfigurierten Arbeitsablaufs. Ihre tatsächliche Durchführung oder das erfolgreiche Öffnen einer konkreten Datei wird durch diesen Vermerk nicht nachgewiesen.

Die Ergebnisse sind eine natürlichsprachliche technische Beschreibung und eine BPMN-Datei zur Darstellung und Bearbeitung im Modellierungseditor. Die Bereitstellung in einer Prozesslaufzeitumgebung, die Implementierung der beschriebenen Dienste und die Ausführung des Datenverarbeitungsprozesses sind nicht als Arbeitsschritte beschrieben.

## 5. Verantwortung und fachliche Grenzen

Der Agent unterstützt die Erstellung technischer Prozessentwürfe und Modelle. Die Feststellung der tatsächlich eingesetzten Systeme, Schnittstellen, Datenstrukturen und Verarbeitungsregeln ist davon zu unterscheiden. Die zuständigen Personen verantworten die Bestätigung dieser Angaben und die Verwendung des Modells. Ein verbindlicher Freigabe-, Pflege- oder Betriebsprozess ist in der I-Agentenanweisung nicht festgelegt.

Die ausschließliche IT-Perspektive bildet technische Datenverarbeitung und Systembeziehungen ab. Tätigkeiten von Bürgern, Behörden oder Fachbereichen werden nicht als eigene Beteiligten-Pools modelliert. Der sequentielle Happy Path umfasst zudem keine Fehlerbehandlung, Alternativpfade oder parallele Abläufe. Die verlangte explizite Darstellung technischer Schritte ist daher keine Aussage über die vollständige Abbildung sämtlicher Betriebs- und Verfahrensvarianten.

Die Darstellung eines Service Tasks, Script Tasks oder einer Schnittstelle ist keine Implementierung des jeweiligen Dienstes, Skripts oder Datenaustauschs. Für den tatsächlichen Betrieb wären unter anderem technische Komponenten, Schnittstellenkonfigurationen, Datenhaltung, Berechtigungen und die Einbindung in eine Laufzeitumgebung gesondert umzusetzen. Aus der Erzeugung einer BPMN-Datei kann für sich genommen keine produktive Ausführbarkeit abgeleitet werden.

Auch modellierte Validierungs- oder Geschäftsregeln begründen keine Feststellung, dass Daten im realen System entsprechend geprüft werden. Personenbezogene Daten, Zugriffsrechte und rechtliche Anforderungen an die Verarbeitung sind im weiteren fachlichen und technischen Verfahren gesondert zu behandeln. Dieser Vermerk dokumentiert die konfigurierte Unterstützung bei der Modellierung, nicht eine fachliche Freigabe oder eine Freigabe zum produktiven Betrieb.

## 6. Quellengrundlage

Grundlage sind die folgenden Projektunterlagen in der zum Dokumentationszeitpunkt eingesehenen Fassung:

- [.github/agents/GovModeler_I.agent.md](.github/agents/GovModeler_I.agent.md): Agentenkonfiguration, IT-Perspektive, Datenverarbeitungsbeschreibung, Referenzsuche, Modellstruktur, automatischer Workflow und Abschlussprüfungen.
- [BPMN_Template.xml](BPMN_Template.xml): vorgeschriebene technische Strukturreferenz; die systemspezifische Poolstruktur wird durch die I-Agentenanweisung festgelegt.
- [BPMN-DI_Guidelines.md](BPMN-DI_Guidelines.md): Vorgaben zu Diagrammelementen, Positionierung, Abmessungen und Verbindungsführung.
- [TECHNISCHE_DOKUMENTATION.md](TECHNISCHE_DOKUMENTATION.md): technische Voraussetzungen, Modellauswahl, Agentennutzung und Modellierungseditor.
- [README.md](README.md): Projektkontext der KI-gestützten Prozessmodellierung in der öffentlichen Verwaltung.