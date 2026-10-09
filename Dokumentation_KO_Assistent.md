# Aktenvermerk: Technische und fachliche Umsetzung des Agenten KO

**Themenfeld:** Prozessmanagement und künstliche Intelligenz  
**Dokumentationsstand:** 09.10.2026  
**Gegenstand:** Erstellung von Prozessbeschreibungen und BPMN-Modellen durch den Custom Agent GovModeler_KO in Visual Studio Code mit GitHub Copilot

## 1. Anlass und Zielsetzung

Der Agent KO unterstützt im Projekt GovModeler die Beschreibung und Modellierung von Verwaltungsprozessen aus den Perspektiven Kunde und Organisation. Die Organisation wird in der Agentenanweisung als Behörde beziehungsweise Organisation konkretisiert. Ausgehend von einem Prozessnamen soll zunächst eine strukturierte Ablaufbeschreibung entstehen. Nach Bestätigung durch die anfragende Person ist die Überführung in ein Modell nach Business Process Model and Notation (BPMN) vorgesehen.

Der Bezug zum Prozessmanagement besteht in der Darstellung der Aktivitäten auf Kunden- und Organisationsseite sowie des Nachrichtenaustauschs zwischen beiden Beteiligtenbereichen. Der Prozess soll ausdrücklich vom Kunden aus beschrieben werden. Die KI übernimmt die sprachliche Ausarbeitung der Beschreibung und deren Übersetzung in eine technische Modellstruktur. Ein eigener IT-Pool ist im vorgesehenen Zwei-Pool-Modell nicht enthalten.

Ziel ist die Bereitstellung einer Prozessbeschreibung und einer bearbeitbaren BPMN-Datei als Grundlage für die weitere fachliche und technische Bearbeitung. Der Agent führt den beschriebenen Verwaltungsvorgang nicht selbst aus und trifft keine Entscheidung über einen Antrag. Dieser Vermerk beschreibt die hinterlegte Konfiguration und den vorgesehenen Bearbeitungsablauf. Eine Bewertung oder Evaluation des Agenten ist nicht Gegenstand.

## 2. Fachliche Umsetzung und Wissensbasis

Ausgangspunkt ist ein von der anfragenden Person genannter Prozessname. Die Agentenanweisung verlangt zunächst eine Zusammenfassung in zwei bis drei Sätzen zum Prozesszweck und zu den beteiligten Akteuren. Anschließend sollen die Prozessschritte chronologisch beschrieben und nach den Pools Kunde und Behörde gruppiert werden. Jeder Schritt erhält eine Nummer, einen Namen nach dem Muster „Substantiv + Verb“, eine Akteursangabe und eine kurze Aktivitätsbeschreibung. Beim Nachrichtenaustausch soll die Richtung zwischen den Akteuren ausdrücklich benannt werden.

Der Darstellungsumfang ist auf den regulären, erfolgreichen Ablauf beschränkt, den die Agentenanweisung als „Happy Path“ bezeichnet. Alternativpfade, Fehlerfälle und parallele Abläufe sind nicht vorgesehen. Sämtliche Prozessschritte sollen nacheinander erfolgen. Eine zahlenmäßige Obergrenze für die Schritte je Pool ist in der KO-Agentenanweisung nicht festgelegt.

Das Startereignis soll im Perfekt formuliert werden, beispielsweise als „Antrag eingegangen“. Das Endereignis wird im Perfekt oder als Zustand benannt. Für die Beschreibung ist ein förmlicher und wissenschaftlicher Kommunikationsstil vorgesehen. Die Kundenperspektive und die klare Benennung der Nachrichtenflüsse bilden ausdrückliche fachliche Darstellungsregeln.

Die für KO maßgeblichen Informationsquellen haben unterschiedliche Funktionen:

- **Agentenanweisung:** Rolle, Kundenperspektive, Darstellungsumfang, Prozessbeschreibungsregeln, technische Vorgaben und Arbeitsschritte.
- **Prozessangabe der anfragenden Person:** Ausgangspunkt für den zu beschreibenden Verwaltungsvorgang.
- **BPMN-Vorlage:** in der Agentenanweisung vorgeschriebene Strukturreferenz für die Kollaboration zwischen Kunde und Organisation.
- **BPMN-DI-Richtlinien:** in der Agentenanweisung vorgeschriebene Referenz für die Diagrammdarstellung und das Layout.
- **Projektdokumentation:** Einordnung der KI-gestützten Prozessmodellierung und Nutzung über Copilot Chat.

Vor der Modellerstellung verlangt die Agentenanweisung das erfolgreiche Lesen beider Referenzdokumente. Sie enthält hierfür konkrete Repository-Adressen, die auf den Stand `1-auswahl-der-pools-koi` verweisen. Diese Referenzen dienen nach der Anweisung der technischen Strukturierung und Darstellung. Eine verbindliche verfahrensspezifische oder rechtliche Wissensquelle ist nicht festgelegt. Die erzeugte Beschreibung ist daher von einer anhand örtlicher Zuständigkeiten und einschlägiger Vorschriften bestätigten Verfahrensbeschreibung zu unterscheiden.

## 3. Technische Umsetzung

KO ist als Custom Agent in Visual Studio Code mit GitHub Copilot konfiguriert. Die [Agentendatei](.github/agents/GovModeler_KO.agent.md) besteht aus einem YAML-Kopf mit Einsatzbeschreibung und Werkzeugauswahl sowie einem Anweisungstext. Die Einsatzbeschreibung nennt die Prozessbeschreibung in den Pools Kunde und Organisation. Der Anweisungstext legt die Rolle eines auf Verwaltungsprozesse spezialisierten BPMN-Modellierers fest.

Die Werkzeugauswahl umfasst das Erstellen und Lesen von Dateien, Suchfunktionen sowie Terminalausführung und den Zugriff auf Terminalausgaben. Damit ist die Konfiguration auf die Verarbeitung von Projektunterlagen und die Erzeugung von Modelldateien ausgerichtet. Diese Angaben beschreiben die verfügbaren Werkzeuge und das vorgesehene Vorgehen; dieser Vermerk dokumentiert keinen konkreten Ausführungslauf.

Als technisches Ergebnis ist eine XML-Datei mit der Endung `.bpmn` vorgesehen. Neben den Prozess- und Kollaborationselementen soll sie Diagramminformationen nach BPMN Diagram Interchange (BPMN-DI) enthalten. Diese beschreiben die sichtbare Anordnung der Elemente und die Führung ihrer Verbindungen. Die Agentenanweisung verlangt die Verwendung der Vorlagenstruktur und die Beachtung der Darstellungsrichtlinien.

Das Modell besteht aus dem Kunden-Pool oben und dem Organisations- beziehungsweise Behörden-Pool unten. Die Anweisung legt Poolbreiten von 1200 Pixeln, Poolhöhen von 250 bis 300 Pixeln und feste vertikale Positionen fest. Aufgaben innerhalb eines Pools werden horizontal ausgerichtet. Für Aufgaben, Ereignisse und gegebenenfalls weitere Elemente sind typabhängige Koordinaten vorgegeben; zwischen Aufgaben ist ein horizontaler Positionsabstand von 160 Pixeln vorgesehen.

Manuelle Bearbeitungen sollen als User Tasks, automatische Prüfungen als Service Tasks dargestellt werden. Message Events und Message Flows bilden den Nachrichtenaustausch zwischen Kunde und Organisation ab, beispielsweise Antrag und Bescheid. Die Darstellung als Service Task beschreibt den vorgesehenen Aufgabentyp im Modell, nicht die Implementierung eines ausführbaren Dienstes. Auch ohne eigenen IT-Pool sieht die Anweisung somit die Darstellung automatisierter Prüfungen vor.

Die Ausgabe ist im Ordner CreateBPMN mit einem sprechenden, prozessbezogenen Dateinamen vorgesehen. Als Beispiel nennt die Anweisung `Personalausweis_beantragen.bpmn`. In den BPMN-Elementen sind Umlaute und ß durch ae, oe, ue und ss zu ersetzen. Die technische Projektdokumentation nennt GitHub Copilot und Copilot Chat für die KI-Interaktion sowie den Camunda Modeler für die Darstellung und Bearbeitung der Modelle.

Die Umsetzung verbindet das Sprachmodell zur Interpretation und Generierung, die Agentenanweisung zur Steuerung des Vorgehens und dateibasierte Referenzen für die Modellstruktur. Die Modellierungsregeln sind als natürlichsprachliche Vorgaben formuliert. Eine separate programmatische Durchsetzung dieser Regeln ist in der Agentendatei nicht implementiert. Ein eigenes Training auf den Projektunterlagen, eine separate Vektordatenbank oder eine eigenständig implementierte Retrieval-Pipeline sind in den herangezogenen Unterlagen nicht beschrieben.

Ein bestimmtes KI-Modell oder eine Modellversion ist in der KO-Agentendatei nicht festgelegt. Die technische Dokumentation sieht die Modellauswahl in Copilot Chat vor. Hosting, Speicherung von Eingaben und betriebliche Datenschutzregelungen werden in der Agentendatei nicht beschrieben; hierzu trifft dieser Vermerk keine weitergehenden Feststellungen.

## 4. Bearbeitungsablauf und Ausgabe

Die Interaktion erfolgt über Copilot Chat. Nach der technischen Projektdokumentation werden das KI-Modell und der Agent ausgewählt und anschließend der Prozess benannt. Die KO-Agentenanweisung sieht folgenden Ablauf vor:

1. **Prozessbeschreibung erstellen:** Eine Zusammenfassung und eine detaillierte Beschreibung mit Startereignis, chronologischen Aktivitäten und Endereignis formulieren. Die Schritte nach Kunde und Organisation gruppieren und die Nachrichtenrichtungen benennen.
2. **Darstellungsrahmen erläutern:** Darauf hinweisen, dass grundsätzlich ein Modell mit zwei Pools vorgesehen ist. Die anfragende Person kann einen abweichenden Darstellungswunsch angeben.
3. **Bestätigung einholen:** Nachfragen, ob ein BPMN-XML-Modell erstellt werden soll.
4. **Voraussetzungen prüfen:** Nach Bestätigung prüfen, ob der Ausgabeordner CreateBPMN existiert; falls nicht, die anfragende Person informieren. Beide Referenzdokumente erfolgreich lesen und sicherstellen, dass die Vorlagenstruktur verfügbar ist.
5. **Modell erstellen:** Die Beschreibung in die Zwei-Pool-Struktur überführen und Aufgaben, Ereignisse, Nachrichtenflüsse sowie Diagramminformationen nach den vorgegebenen Regeln anlegen.
6. **Datei ablegen und Vorgaben prüfen:** Das Modell unter einem prozessbezogenen Namen mit der Endung `.bpmn` im vorgesehenen Ordner speichern und die aufgeführten Abschlussprüfungen vornehmen.

Die vorgesehenen Abschlussprüfungen betreffen unter anderem das erfolgreiche Lesen der Referenzen, das Vorhandensein des Ausgabeordners, die Zwei-Pool-Struktur, die horizontale Anordnung, den Happy Path, die Umlautersetzung, Nachrichtenflüsse, Poolabmessungen sowie Dateiname und Ablageort. Sie gehören zum konfigurierten Arbeitsablauf. Eine tatsächliche Durchführung dieser Prüfungen wird durch diesen Vermerk nicht nachgewiesen.

Die erste Ausgabe ist eine natürlichsprachliche Prozessbeschreibung. Erst nach Zustimmung zur Modellgenerierung ist zusätzlich eine BPMN-Datei vorgesehen. Die Beschreibung, die technische Modelldatei und deren Darstellung im Modellierungseditor sind unterschiedliche Bestandteile der Bearbeitung. Eine Bereitstellung oder Ausführung in einer Prozesslaufzeitumgebung ist nicht als Arbeitsschritt beschrieben.

## 5. Verantwortung und fachliche Grenzen

Der Agent unterstützt die Erstellung von Prozessentwürfen und technischen Modellen. Die Feststellung des tatsächlich geltenden Ablaufs, der örtlichen Zuständigkeiten und der fachlichen beziehungsweise rechtlichen Anforderungen ist davon zu unterscheiden. Die zuständigen Personen verantworten die fachliche Bestätigung und die Verwendung des Modells im weiteren Prozessmanagement. Ein verbindlicher Freigabe-, Pflege- oder Betriebsprozess ist in der KO-Agentenanweisung nicht festgelegt.

Die Beschränkung auf den sequentiellen Happy Path legt den vorgesehenen Darstellungsumfang fest. Ausnahmebehandlungen, parallele Bearbeitungen und weitere Verfahrensvarianten sind nicht Gegenstand des regulären Modellierungsauftrags. Aus dem Modell kann daher keine vollständige Abbildung sämtlicher Varianten eines Verwaltungsverfahrens abgeleitet werden. Die Zwei-Pool-Struktur bildet Kunden- und Organisationsseite ab; eine gesonderte Darstellung der IT als eigenständiger Beteiligtenbereich ist nicht vorgesehen.

Die Modellierung einer automatischen Prüfung ist keine technische Umsetzung dieser Prüfung. Für eine tatsächliche Automatisierung wären gegebenenfalls ausführbare Dienste, Schnittstellen, Datenhaltung, Berechtigungen und die Einbindung in eine Laufzeitumgebung gesondert umzusetzen. Die Erzeugung einer BPMN-Datei begründet für sich genommen keine Feststellung ihrer produktiven Ausführbarkeit.

Die fachliche Beschreibung und die technische Modellierung bleiben an die Eingaben und die hinterlegten Vorgaben gebunden. Änderungen am tatsächlichen Verfahren oder an den Modellierungsstandards müssen bei der weiteren Bearbeitung berücksichtigt werden. Der Vermerk dokumentiert die konfigurierte Unterstützung bei der Modellierung, nicht eine fachliche Freigabe oder eine Freigabe zum produktiven Betrieb.

## 6. Quellengrundlage

Grundlage sind die folgenden Projektunterlagen in der zum Dokumentationszeitpunkt eingesehenen Fassung:

- [.github/agents/GovModeler_KO.agent.md](.github/agents/GovModeler_KO.agent.md): Agentenkonfiguration, Kundenperspektive, Prozessbeschreibungsregeln, Modellierungsumfang, Workflow, Ausgabe und Abschlussprüfungen.
- [TECHNISCHE_DOKUMENTATION.md](TECHNISCHE_DOKUMENTATION.md): technische Voraussetzungen, Modellauswahl und Nutzung über Copilot Chat.
- [README.md](README.md): Projektkontext der KI-gestützten Prozessmodellierung in der öffentlichen Verwaltung.

Die Agentenanweisung benennt zusätzlich eine BPMN-Vorlage und BPMN-DI-Richtlinien unter konkreten Repository-Adressen zum Stand `1-auswahl-der-pools-koi`. Diese verlinkten Fassungen konnten für die Erstellung dieses Vermerks nicht eigenständig eingesehen werden. Aussagen über ihre vorgesehene Funktion beruhen deshalb auf der KO-Agentenanweisung; ihr tatsächlicher Inhalt wird hier nicht beschrieben oder bewertet. Die im aktuellen Workspace vorhandenen gleichnamigen Unterlagen werden nicht als Nachweis für den Inhalt dieser verlinkten Fassungen verwendet.