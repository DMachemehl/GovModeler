# Aktenvermerk: Technische und fachliche Umsetzung des Agenten KOI

**Themenfeld:** Prozessmanagement und künstliche Intelligenz  
**Dokumentationsstand:** 09.10.2026  
**Gegenstand:** Erstellung von Prozessbeschreibungen und BPMN-Modellen durch den Custom Agent GovModeler_KOI in Visual Studio Code mit GitHub Copilot

## 1. Anlass und Zielsetzung

Der Agent KOI unterstützt im Projekt GovModeler die Beschreibung und Modellierung von Verwaltungsprozessen. Die Bezeichnung KOI steht für die Perspektiven Kunde, Organisation und IT. Die Agentenanweisung konkretisiert diese Perspektiven durch drei Beteiligtenbereiche: Bürger, Behörde beziehungsweise Organisation und IT. Ausgehend von einem Prozessnamen soll der Agent zunächst eine strukturierte Ablaufbeschreibung erstellen und diese nach Bestätigung durch die anfragende Person in ein BPMN-Modell überführen.

Der Bezug zum Prozessmanagement besteht in der Darstellung von Aktivitäten, beteiligten Akteuren und Nachrichtenbeziehungen innerhalb eines Verwaltungsvorgangs. Die KI übernimmt die sprachliche Ausarbeitung der Prozessbeschreibung und deren Übersetzung in eine technische Modellstruktur nach Business Process Model and Notation (BPMN). Die drei Perspektiven sollen dabei gemeinsam betrachtet und als zusammenhängende Kollaboration dargestellt werden.

Ziel ist die Bereitstellung einer Prozessbeschreibung und einer bearbeitbaren BPMN-Datei als Grundlage für die weitere fachliche und technische Bearbeitung. Der Agent führt den beschriebenen Verwaltungsprozess nicht selbst aus. Dieser Vermerk beschreibt die hinterlegte Konfiguration, die verwendeten Referenzunterlagen und den vorgesehenen Bearbeitungsablauf. Eine Bewertung oder Evaluation des Agenten ist nicht Gegenstand.

## 2. Fachliche Umsetzung und Wissensbasis

Ausgangspunkt ist ein von der anfragenden Person genannter Prozessname. Die Agentenanweisung verlangt zunächst eine kurze Zusammenfassung zum Prozesszweck und zu den beteiligten Akteuren. Anschließend sollen die Aktivitäten chronologisch beschrieben und nach den drei Beteiligtenbereichen gruppiert werden. Für jeden Schritt sind eine Nummer, eine Bezeichnung nach dem Muster „Substantiv + Verb“, der Akteur und eine kurze Aktivitätsbeschreibung vorgesehen. Beim Nachrichtenaustausch soll die Richtung zwischen den Akteuren ausdrücklich benannt werden.

Der fachliche Darstellungsumfang ist auf den regulären, erfolgreichen Ablauf beschränkt, den die Agentenanweisung als „Happy Path“ bezeichnet. Alternativpfade, Fehlerfälle und parallele Abläufe sind nicht vorgesehen. Die Schritte sollen nacheinander erfolgen; je Pool sind höchstens fünf Schritte vorgegeben. Das Startereignis wird im Perfekt, das Endereignis im Perfekt oder als Zustand formuliert. Für die Prozessbeschreibung ist ein förmlicher und wissenschaftlicher Kommunikationsstil festgelegt.

Die Zuordnung zu den Beteiligtenbereichen folgt einer ausdrücklich auf Digitalisierung ausgerichteten Modellierungsregel: Aufgaben, die digitalisiert oder automatisiert werden können, sollen im IT-Pool dargestellt werden. Diese Zuordnung beschreibt die vorgesehene Modellierungsperspektive. Sie belegt nicht, dass die betreffende Aufgabe im tatsächlichen Verwaltungsverfahren bereits automatisiert ist oder dass eine entsprechende technische Umsetzung besteht.

Die für KOI maßgeblichen Informationsquellen haben unterschiedliche Funktionen:

- **Agentenanweisung:** Rolle, Darstellungsumfang, Prozessbeschreibungsregeln, Modellierungsvorgaben, Arbeitsschritte und Ausgabeort.
- **Prozessangabe der anfragenden Person:** Ausgangspunkt für den zu beschreibenden Verwaltungsvorgang.
- **BPMN-Vorlage:** technische Strukturreferenz für die Kollaboration mit Bürger-, IT- und Behörden-Pool.
- **BPMN-DI-Richtlinien:** Vorgaben zur Diagrammdarstellung, Anordnung der Elemente und Führung der Verbindungen.
- **Projektdokumentation:** Einordnung des KOI-Ansatzes und Nutzung über Copilot Chat.

Vor der Erstellung des BPMN-Modells verlangt die Agentenanweisung ausdrücklich das Lesen der BPMN-Vorlage und der BPMN-DI-Richtlinien. Diese Unterlagen dienen der technischen Strukturierung und Darstellung. Eine verbindliche verfahrensspezifische oder rechtliche Wissensquelle ist in der Agentenanweisung nicht festgelegt. Die erzeugte Prozessbeschreibung ist daher von einer anhand örtlicher Zuständigkeiten und einschlägiger Vorschriften bestätigten Verfahrensbeschreibung zu unterscheiden.

## 3. Technische Umsetzung

KOI ist als Custom Agent in Visual Studio Code mit GitHub Copilot konfiguriert. Die [Agentendatei](.github/agents/GovModeler_KOI.agent.md) besteht aus einem YAML-Kopf mit Einsatzbeschreibung und Werkzeugauswahl sowie einem Anweisungstext. Die Einsatzbeschreibung benennt die Prozessbeschreibung in den Pools Kunde, Organisation und IT. Der Anweisungstext legt die Rolle eines auf Verwaltungsprozesse spezialisierten BPMN-Modellierers fest.

Die Werkzeugauswahl umfasst das Erstellen von Dateien, das Lesen von Dateien, Suchfunktionen sowie Terminalausführung und den Zugriff auf Terminalausgaben. Damit ist die Konfiguration auf die Verarbeitung von Projektunterlagen und die Erzeugung von Modelldateien ausgerichtet. Die konfigurierten Werkzeuge und Arbeitsschritte beschreiben das vorgesehene Vorgehen; dieser Vermerk dokumentiert keinen konkreten Ausführungslauf.

Das technische Ergebnis ist eine XML-Datei mit der Endung `.bpmn`. Neben den Prozess- und Kollaborationselementen sind Diagramminformationen nach BPMN Diagram Interchange (BPMN-DI) vorgesehen. Diese enthalten die Positionen und Größen der sichtbaren Elemente sowie die Wegpunkte ihrer Verbindungen. Die Agentenanweisung verlangt die Nutzung der Struktur aus der BPMN-Vorlage und die Beachtung der BPMN-DI-Richtlinien.

Die drei Pools werden von oben nach unten in der Reihenfolge Bürger, IT und Behörde angeordnet. Für die Darstellung sind feste Poolabmessungen, Koordinaten und Abstände vorgegeben. Aufgaben innerhalb eines Pools sollen horizontal ausgerichtet werden. Manuelle Bearbeitungen werden als User Tasks, automatische Prüfungen als Service Tasks dargestellt. Message Events und Message Flows bilden den Nachrichtenaustausch zwischen den Pools ab, beispielsweise Antrag und Bescheid zwischen Bürger und Behörde oder Datenanfragen und Antworten zwischen Behörde und IT.

Die Dateiausgabe ist im Ordner CreateBPMN mit einem sprechenden, prozessbezogenen Namen vorgesehen. Als Beispiel nennt die Anweisung `Personalausweis_beantragen.bpmn`. In den BPMN-Elementen sind Umlaute und ß durch ae, oe, ue und ss zu ersetzen. Die technische Projektdokumentation nennt GitHub Copilot und Copilot Chat für die KI-Interaktion sowie den Camunda Modeler für die Darstellung und Bearbeitung der Modelle.

Die Umsetzung verbindet das Sprachmodell zur Interpretation und Generierung, die Agentenanweisung zur Steuerung des Vorgehens und die dateibasierten Referenzen zur Strukturierung des Ergebnisses. Die Modellierungsregeln sind als natürlichsprachliche Vorgaben formuliert. Eine separate programmatische Durchsetzung dieser Regeln ist in der Agentendatei nicht implementiert. Ein eigenes Training auf den Projektunterlagen, eine separate Vektordatenbank oder eine eigenständig implementierte Retrieval-Pipeline sind in den herangezogenen Unterlagen nicht beschrieben.

Ein bestimmtes KI-Modell oder eine Modellversion ist in der KOI-Agentendatei nicht festgelegt. Die technische Dokumentation sieht die Modellauswahl in Copilot Chat vor. Hosting, Speicherung von Eingaben und betriebliche Datenschutzregelungen werden in der Agentendatei nicht beschrieben; hierzu trifft dieser Vermerk keine weitergehenden Feststellungen.

## 4. Bearbeitungsablauf und Ausgabe

Die Interaktion erfolgt über Copilot Chat. Nach der technischen Projektdokumentation werden das KI-Modell und der Agent ausgewählt und anschließend der Prozess benannt. Die KOI-Agentenanweisung sieht zwei aufeinander aufbauende Bearbeitungsphasen vor:

1. **Prozessbeschreibung erstellen:** Ausgehend vom Prozessnamen eine Zusammenfassung in zwei bis drei Sätzen und eine detaillierte Beschreibung mit Startereignis, chronologischen Aktivitäten und Endereignis formulieren. Die Aktivitäten werden den drei Pools zugeordnet; Nachrichtenbeziehungen werden ausdrücklich benannt.
2. **Darstellungsrahmen erläutern:** Darauf hinweisen, dass grundsätzlich ein BPMN-Modell mit den drei Pools Bürger, IT und Behörde vorgesehen ist. Die anfragende Person kann einen abweichenden Darstellungswunsch angeben.
3. **Bestätigung einholen:** Nachfragen, ob auf Grundlage der Beschreibung ein BPMN-XML-Modell erstellt werden soll.
4. **Referenzen lesen:** Nach Bestätigung die BPMN-Vorlage und die BPMN-DI-Richtlinien heranziehen.
5. **Modell erstellen:** Die Prozessbeschreibung in die vorgegebene Drei-Pool-Struktur überführen und Aufgaben, Ereignisse, Nachrichtenflüsse sowie Diagramminformationen anlegen.
6. **Datei ablegen und Vorgaben prüfen:** Das Modell unter einem prozessbezogenen Namen mit der Endung `.bpmn` im Ordner CreateBPMN speichern und die in der Anweisung aufgeführten Abschlussprüfungen vornehmen.

Die vorgesehenen Abschlussprüfungen beziehen sich unter anderem auf das Lesen der Referenzen, die Drei-Pool-Struktur, die horizontale Anordnung, die Schrittbegrenzung, die Beschränkung auf den Happy Path, die Umlautersetzung sowie Dateiname und Ablageort. Sie sind Bestandteil des konfigurierten Arbeitsablaufs. Eine Durchführung dieser Prüfungen wird mit diesem Vermerk nicht nachgewiesen.

Die erste Ausgabe ist eine natürlichsprachliche Prozessbeschreibung. Erst nach Zustimmung zur Modellgenerierung ist zusätzlich eine BPMN-Datei vorgesehen. Die textliche Beschreibung, die technische Modelldatei und die spätere Darstellung im Modellierungseditor sind somit unterschiedliche Bestandteile der Bearbeitung. Eine Bereitstellung in einer Prozesslaufzeitumgebung ist nicht als Arbeitsschritt beschrieben.

## 5. Verantwortung und fachliche Grenzen

Der Agent unterstützt die Erstellung von Prozessentwürfen und technischen Modellen. Die Feststellung des tatsächlich geltenden Ablaufs, der örtlichen Zuständigkeiten und der fachlichen beziehungsweise rechtlichen Anforderungen ist davon zu unterscheiden. Die zuständigen Personen verantworten die fachliche Bestätigung und die Verwendung des Modells im weiteren Prozessmanagement. Ein verbindlicher Freigabe-, Pflege- oder Betriebsprozess ist in der KOI-Agentenanweisung nicht festgelegt.

Die Beschränkung auf einen sequentiellen Happy Path mit höchstens fünf Schritten pro Pool legt den Umfang der vorgesehenen Darstellung fest. Ausnahmebehandlungen, parallele Bearbeitungen und weitere Verfahrensvarianten sind damit nicht Gegenstand des regulären Modellierungsauftrags. Aus einem solchen Modell kann keine vollständige Abbildung sämtlicher Varianten eines Verwaltungsverfahrens abgeleitet werden.

Die Darstellung einer Aktivität als Service Task oder ihre Zuordnung zum IT-Pool ist keine Implementierung dieser Aktivität. Für eine tatsächliche Automatisierung wären gegebenenfalls ausführbare Dienste, Schnittstellen, Datenhaltung, Berechtigungen und die Einbindung in eine Laufzeitumgebung gesondert umzusetzen. Ebenso begründet die Erzeugung einer BPMN-Datei für sich genommen keine Feststellung ihrer produktiven Ausführbarkeit.

Die fachliche Beschreibung und die technische Modellierung bleiben an die Eingaben und die hinterlegten Vorgaben gebunden. Änderungen am realen Verfahren oder an den Modellierungsstandards müssen bei der weiteren Bearbeitung berücksichtigt werden. Der Vermerk dokumentiert die konfigurierte Unterstützung bei der Modellierung, nicht eine fachliche Freigabe oder eine Freigabe zum produktiven Betrieb.

## 6. Quellengrundlage

Grundlage sind die folgenden Projektunterlagen in der zum Dokumentationszeitpunkt eingesehenen Fassung:

- [.github/agents/GovModeler_KOI.agent.md](.github/agents/GovModeler_KOI.agent.md): Agentenkonfiguration, Prozessbeschreibungsregeln, Modellierungsumfang, Workflow, Ausgabe und Abschlussprüfungen.
- [BPMN_Template.xml](BPMN_Template.xml): vorgeschriebene Strukturreferenz für die Drei-Pool-Kollaboration einschließlich Nachrichtenflüssen und Diagramminformationen.
- [BPMN-DI_Guidelines.md](BPMN-DI_Guidelines.md): technische Darstellungsregeln, Layoutvorgaben und Verbindungsführung.
- [TECHNISCHE_DOKUMENTATION.md](TECHNISCHE_DOKUMENTATION.md): technische Voraussetzungen, Modellauswahl und Nutzung über Copilot Chat.
- [README.md](README.md): Projektkontext der KI-gestützten Prozessmodellierung und Einbeziehung der Perspektiven Kunde, Organisation und IT.