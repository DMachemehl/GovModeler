# Aktenvermerk: Technische und fachliche Umsetzung des Agenten BPMN Process Studio

**Themenfeld:** Prozessmanagement und künstliche Intelligenz  
**Dokumentationsstand:** 09.10.2026  
**Gegenstand:** Erstellung von Prozessbeschreibungen und BPMN-Modellen für das Zielsystem d.velop Process Studio durch den Custom Agent BPMN_ProcessStudio in Visual Studio Code mit GitHub Copilot

## 1. Anlass und Zielsetzung

Der Agent BPMN Process Studio unterstützt im Projekt GovModeler die Beschreibung und technische Modellierung von Verwaltungsprozessen für die weitere Bearbeitung in d.velop Process Studio. Ausgehend von einem Prozessnamen soll der Agent zunächst eine strukturierte Ablaufbeschreibung erstellen und diese nach Bestätigung durch die anfragende Person in ein BPMN-Modell überführen.

Der Bezug zum Prozessmanagement besteht in der Beschreibung von Prozesszweck, Akteuren, Aktivitäten sowie Prozessanfang und Prozessende. Die generative KI übernimmt die sprachliche Ausarbeitung und die Übertragung in eine technische Modellstruktur nach Business Process Model and Notation (BPMN 2.0). Die Ausrichtung auf Process Studio erfolgt über eine projektspezifische XML-Vorlage mit Angaben zur Ausführbarkeit, zur Aufgabenzuweisung, zu Prozessvariablen und zu optionalen Serviceanbindungen.

Ziel ist die Bereitstellung einer Prozessbeschreibung und einer bearbeitbaren BPMN-Datei, die für die Übernahme in Process Studio und die anschließende Bereitstellung zur Ausführung vorbereitet ist. Der Agent arbeitet dateibasiert in der Projektumgebung. Eine unmittelbare Bedienung von Process Studio oder eine automatische Bereitstellung und Ausführung im Zielsystem ist in seiner Konfiguration nicht eingerichtet.

Dieser Vermerk beschreibt die hinterlegte Konfiguration, die verwendeten Referenzunterlagen und den vorgesehenen Bearbeitungsablauf. Eine Bewertung oder Evaluation des Agenten ist nicht Gegenstand. Ein konkreter Generierungs-, Import-, Bereitstellungs- oder Ausführungslauf wird damit nicht dokumentiert.

## 2. Fachliche Umsetzung und Wissensbasis

Ausgangspunkt ist ein von der anfragenden Person genannter Prozessname. Die Agentenanweisung verlangt zunächst eine Zusammenfassung des Prozesszwecks und der beteiligten Akteure in zwei bis drei Sätzen. Anschließend werden das Startereignis, die chronologisch geordneten Prozessschritte und das Endereignis beschrieben. Das Startereignis wird im Perfekt formuliert, etwa „Antrag eingegangen“. Das Endereignis wird im Perfekt oder als Zustand benannt, etwa „Antrag bearbeitet“ oder „Prozess abgeschlossen“. Für die Prozessbeschreibung ist ein förmlicher und wissenschaftlicher Kommunikationsstil festgelegt.

Der Darstellungsumfang ist auf den regulären, erfolgreichen Ablauf beschränkt, den die Agentenanweisung als „Happy Path“ bezeichnet. Alternativpfade, Fehlerfälle und parallele Abläufe sind nicht vorgesehen. Alle Prozessschritte sollen nacheinander erfolgen. Eine feste Höchstzahl von Aktivitäten und ein verbindliches Benennungsschema für einzelne Tätigkeiten sind in dieser Agentenanweisung nicht festgelegt.

Die Anweisung verlangt eine klare Benennung der Nachrichtenflüsse zwischen Pools. Sie legt jedoch weder eine feste Anzahl von Pools noch eine verbindliche Aufteilung in Kunde, Organisation und IT fest. Die technische Vorlage enthält einen einzelnen Prozess ohne Kollaboration, Teilnehmer oder Lanes. Auch das vorhandene Modell „Stammdaten ändern“ verwendet diese Einzelprozessstruktur. Der allgemeine KOI-Ansatz des Projekts ist deshalb von den konkreten Strukturvorgaben dieses Agenten zu unterscheiden.

Die maßgeblichen Informationsquellen haben unterschiedliche Funktionen:

- **Agentenanweisung:** Rolle, Beschreibungsregeln, Begrenzung auf einen sequentiellen Happy Path, Bestätigungsschritt, verpflichtende Vorlagenlektüre und Ausgabeort.
- **Prozessangabe der anfragenden Person:** Ausgangspunkt für den zu beschreibenden Verwaltungsvorgang.
- **BPMN-Vorlage für Process Studio:** technische Strukturreferenz für ausführbare Prozesse, Benutzeraufgaben, Variablen, optionale Serviceaufrufe und Diagramminformationen.
- **Vorhandenes Prozessmodell:** Beispiel für die Umsetzung eines sequentiellen Ablaufs mit Benutzeraufgaben und BPMN-DI im Ausgabeordner.
- **Beispielprozesse und deren Dokumentation:** ergänzende technische Anschauung für Funktionen von d.velop process sowie Hinweise auf Bereitstellung und Prozessstart.
- **Konfiguration des gesonderten Formularagenten:** ergänzende Grundlage zur Abgrenzung der Formularerstellung und ihrer Verknüpfung mit Benutzeraufgaben.
- **Technische Projektdokumentation und Projektbeschreibung:** Einordnung der KI-gestützten Modellierung und der Nutzung über Copilot Chat.

Vor der Modellgenerierung verlangt die Agentenanweisung ausdrücklich das Lesen von `BPMN_Template.xml`. Die weiteren Unterlagen ergänzen die Quellengrundlage dieses Vermerks; sie sind in der BPMN-Agentenanweisung nicht als verpflichtende Leseschritte aufgeführt.

Eine verbindliche verfahrensspezifische oder rechtliche Wissensquelle ist in der Agentenanweisung nicht festgelegt. Die erzeugte Beschreibung ist daher von einer anhand örtlicher Zuständigkeiten und einschlägiger Vorschriften bestätigten Verfahrensbeschreibung zu unterscheiden.

## 3. Technische Umsetzung für das Zielsystem Process Studio

### 3.1 Agentenkonfiguration und Systemgrenze

BPMN_ProcessStudio ist als Custom Agent in Visual Studio Code mit GitHub Copilot konfiguriert. Die Agentendatei besteht aus einem YAML-Kopf mit Einsatzbeschreibung und Werkzeugauswahl sowie einem natürlichsprachlichen Anweisungstext. Als Einsatzbeschreibung ist die „Erstellung ausführbarer BPMN-Modelle in d.velop Process Studio“ hinterlegt. Die Werkzeugauswahl umfasst Dateierstellung, Lesen, Suche, Terminalausführung und den Zugriff auf Terminalinformationen. Ein spezielles Werkzeug zur direkten Bedienung von Process Studio oder eine vorkonfigurierte API-Anbindung an d.velop process ist darin nicht enthalten.

Die Umsetzung verbindet das Sprachmodell zur Interpretation und Generierung, die Agentenanweisung zur Steuerung des Vorgehens und eine dateibasierte Vorlage zur technischen Strukturierung des Ergebnisses. Eine separate programmatische Durchsetzung der Modellierungsregeln ist in der Agentendatei nicht implementiert. Ein eigenes Training auf den Projektunterlagen, eine separate Vektordatenbank oder eine eigenständig implementierte Retrieval-Pipeline sind in den herangezogenen Unterlagen nicht beschrieben.

Ein bestimmtes KI-Modell oder eine Modellversion ist in der Agentendatei nicht festgelegt. Die technische Projektdokumentation sieht die Modellauswahl in Copilot Chat vor. Eine konkrete Version der eingesetzten Process-Studio-Installation sowie Hosting, Speicherung von Eingaben und betriebliche Datenschutzregelungen sind in der Agentenanweisung nicht beschrieben; hierzu trifft dieser Vermerk keine weitergehenden Feststellungen.

### 3.2 Austauschformat und XML-Konventionen

Das technische Ergebnis ist eine XML-Datei mit der Endung `.bpmn`. Die Vorlage legt UTF-8 als Zeichenkodierung fest und enthält sowohl die fachliche BPMN-Struktur als auch Diagramminformationen nach BPMN Diagram Interchange (BPMN-DI). Für die Ausrichtung auf Process Studio sind insbesondere folgende Konventionen hinterlegt:

| Bestandteil | Umsetzung in der Vorlage |
|---|---|
| BPMN-Modellnamensraum | `http://www.omg.org/spec/BPMN/20100524/MODEL` |
| Camunda-Erweiterungsnamensraum | `http://camunda.org/schema/1.0/bpmn` |
| Diagrammnamensräume | BPMN-DI sowie die OMG-Namensräume für Koordinaten und Verbindungen mit den Präfixen `bpmndi`, `dc` und `di` |
| Exporter-Angabe | `exporter="d.velop process modeler"` |
| Exporter-Version | `exporterVersion="1.0.0"` |
| Zielnamensraum | `targetNamespace=""` |
| Prozessdefinition | `<process>` mit eindeutiger ID, Anzeigename und `isExecutable="true"` |
| Kennungen | eindeutige IDs; für neu zu vergebende IDs sieht die Vorlage snake_case vor, beispielsweise `task_approve_request` |

Die Exporter-Angaben kennzeichnen die vorgesehene Dateikonvention. Sie belegen weder, dass die Datei tatsächlich mit dem d.velop process modeler erzeugt wurde, noch welche Produktversion im Zielsystem installiert ist. Die Camunda-Namensräume dienen hier der Beschreibung von Erweiterungsattributen und sind für sich genommen kein Nachweis einer bestimmten technischen Architektur der Zielinstallation.

Im Unterschied zu einem ausschließlich beschreibenden Modell ist der Prozess durch `isExecutable="true"` für die Ausführung gekennzeichnet. Diese Kennzeichnung allein stellt jedoch weder eine erfolgte Bereitstellung noch die tatsächliche Ausführbarkeit in einer konkreten Umgebung fest. Hierfür müssen unter anderem referenzierte Identitäten, Formulare, Variablen und gegebenenfalls Dienste im Zielsystem passend eingerichtet sein.

### 3.3 Prozessstruktur und Benutzeraufgaben

Die Grundstruktur der Vorlage besteht aus einem Startereignis, einer Benutzeraufgabe, einem Endereignis und den verbindenden Sequenzflüssen. Für den Hauptprozess sieht die Vorlage genau ein Startereignis und mindestens ein Endereignis vor. `<sequenceFlow>`-Elemente verbinden die Schritte über `sourceRef` und `targetRef`. Bei der Generierung sind die Platzhalter für Prozess-ID, Prozessname und Aufgabenname zu ersetzen sowie die erforderlichen Aktivitäten und Verbindungen einzufügen.

Menschlich auszuführende Tätigkeiten werden als `<userTask>` modelliert. Die Vorlage enthält hierfür unter anderem folgende Erweiterungsattribute:

- `camunda:candidateUsers="${variables.get('dv_initiator')}"`: vorgesehene Zuweisung über die Variable der prozessinitiierenden Person.
- `camunda:priority="50"`: Prioritätswert der Beispielaufgabe; die Vorlage beschreibt einen Wertebereich von 1 bis 100.
- `camunda:dueDate`: optionale Angabe eines Fälligkeitsdatums.
- `camunda:formKey`: optionale Referenz auf ein Formular.

Das vorhandene Modell „Stammdaten ändern“ enthält sieben nacheinander angeordnete Benutzeraufgaben, darunter „Antrag prüfen“, „Identität verifizieren“ und „Stammdaten aktualisieren“. Alle sind mit der Zuweisung über `dv_initiator` und der Priorität 50 versehen. Dieses Modell veranschaulicht die technische Dateistruktur; es ist kein Nachweis eines tatsächlich eingerichteten Verwaltungsverfahrens oder eines erfolgreichen Prozesslaufs. Die Zuweisung an die initiierende Person ersetzt insbesondere keine gesondert festgelegte fachliche Rollen- und Berechtigungskonzeption.

### 3.4 Prozessvariablen und Serviceanbindungen

Prozessvariablen können in `<extensionElements>` über `<camunda:properties>` und einzelne `<camunda:property>`-Einträge beschrieben werden. Die Vorlage verwendet dafür das Namensmuster `variable:variablenname` und einen Datentyp als Wert. Ein Stern am Ende des Variablennamens kennzeichnet nach der Vorlage eine beim Prozessstart abzufragende Eingabevariable; ein Ausrufezeichen am Datentyp kennzeichnet ein Pflichtfeld. Beispielsweise steht `name="variable:eingabe_text*" value="String!"` für eine verpflichtende Texteingabe beim Start.

Als Typen nennt die Vorlage unter anderem `String`, `Number`, `Boolean`, `Date` und `Identity` sowie Listen von Zeichenketten oder Identitäten. Ausdrücke wie `${variables.get('varname')}` dienen dem Zugriff auf Variablen, beispielsweise für Aufgabenbezeichnungen oder Zuweisungen. Die Variableneinträge in der Vorlage sind auskommentierte Beispiele und werden nicht allein durch das Vorhandensein der Vorlage Bestandteil eines erzeugten Prozesses.

Für externe Serviceaufrufe enthält die Vorlage ein optionales Muster für einen synchronen Dienst. Dieses wird technisch als `<sendTask>` mit `camunda:delegateExpression="${syncService}"` dargestellt. Weitere Attribute sind `camunda:asyncBefore="true"`, `camunda:asyncAfter="true"` und `camunda:exclusive="true"`. Die Kennzeichnung des Dienstes als synchron und diese zusätzlichen Ausführungsattribute sind getrennte Angaben der Vorlage.

Die Serviceadresse wird innerhalb von `<camunda:inputOutput>` als Eingabeparameter `service.uri` hinterlegt, beispielsweise unter einem Pfad nach dem Muster `/process/services/[SERVICE_PATH]/sync`. Weitere Ein- und Ausgabeparameter beschreiben die Übergabe von Daten zwischen Prozess und Dienst. Ergänzende Prozesseigenschaften mit Namen wie `service:/process/services/[SERVICE_PATH]/sync:in:[INPUT_PARAM]` beschreiben Parameter und Dienstbezeichnung. Der Beispielprozess „Sync Service“ zeigt diese Struktur anhand eines Hello-World-Dienstes.

Die Erzeugung dieser XML-Einträge richtet keinen Dienst ein und stellt keine Verbindung zu einem Fachverfahren her. Die Bereitstellung des Dienstes, dessen Erreichbarkeit und die erforderlichen Berechtigungen gehören zur gesonderten technischen Umsetzung im Zielsystem.

Die Vorlage enthält außerdem auskommentierte Muster für Gateways, Timer, Mehrfachausführungen und ereignisgesteuerte Unterprozesse. Diese technischen Möglichkeiten erweitern nicht automatisch den Auftrag des Agenten: Maßgeblich bleibt dessen Beschränkung auf einen sequentiellen Happy Path ohne Alternativpfade, Fehlerfälle und parallele Abläufe.

### 3.5 Diagrammdarstellung

Die sichtbare Darstellung wird über `BPMNDiagram`, `BPMNPlane`, `BPMNShape` und `BPMNEdge` beschrieben. Die Diagrammebene verweist mit `bpmnElement` auf den Prozess. Entsprechende Referenzen verbinden Formen und Kanten mit den fachlichen BPMN-Elementen. Positionen und Größen stehen in `dc:Bounds`; Verbindungslinien werden durch `di:waypoint` beschrieben.

Die Vorlage nennt folgende Standardwerte:

| Element oder Anordnung | Vorgabe |
|---|---|
| Start- und Endereignisse | Breite 36, Höhe 36 |
| Aufgaben | Breite 100, Höhe 80 |
| Gateways, falls verwendet | Breite 50, Höhe 50 |
| Angeheftete Ereignisse, falls verwendet | Breite 36, Höhe 36 |
| Mindestabstand zwischen Elementen | 60 |
| Anordnung der Aufgaben | horizontal mit gleicher Y-Koordinate |
| Ereignisse | auf der Mittellinie der Aufgaben |

Diese Angaben betreffen die Koordinaten und Abmessungen des BPMN-DI-Layouts; die Vorlage bezeichnet Abstände als Pixelwerte. Bei zusätzlichen Aktivitäten sind die Diagrammformen und Verbindungskanten entsprechend zu ergänzen. Die Datei enthält dadurch neben der Ablaufstruktur auch die Informationen für deren visuelle Darstellung. Eine Prüfung der Darstellung in einer konkreten Process-Studio-Installation wird mit diesem Vermerk nicht dokumentiert.

### 3.6 Formularanbindung und Abgrenzung zum Formularagenten

Die BPMN-Vorlage sieht mit `camunda:formKey` eine optionale Formularreferenz an Benutzeraufgaben vor. Die eigentliche Formularerstellung ist im Projekt einem gesonderten Custom Agent, Form_ProcessStudio, zugeordnet. Dessen Konfiguration beschreibt die Erzeugung von Formularen im JSON-Format auf Grundlage von Form.io und den im Projekt dokumentierten Vorgaben für die d.velop Forms API.

Nach dieser Konfiguration werden Formular-Dateien im Ordner `CreateForm/` abgelegt. Der Formularagent erzeugt eine Formular-ID und trägt sie als `camunda:formKey` an der betreffenden Benutzeraufgabe in der angegebenen BPMN-Datei ein. Hierfür benötigt er unter anderem den BPMN-Dateipfad, die Aufgaben-ID sowie Angaben zu Formularzweck und Feldern.

Diese Verknüpfung ist ein ergänzender Projektworkflow und keine ausdrücklich festgelegte Aufgabe des BPMN-Agenten. Ein in der BPMN-Datei eingetragener Formularschlüssel belegt zudem noch nicht, dass das Formular in der Zielinstallation verfügbar ist. Die Übernahme des Formulars und die Übereinstimmung seiner Kennung mit der Prozessreferenz sind von der dateibasierten Erstellung zu unterscheiden.

## 4. Bearbeitungsablauf und Ausgabe

Die Interaktion erfolgt über Copilot Chat in Visual Studio Code. Die technische Projektdokumentation sieht die Auswahl eines KI-Modells und eines Agenten sowie die anschließende Benennung des Prozesses vor. Für BPMN_ProcessStudio ist folgender Ablauf hinterlegt beziehungsweise in den ergänzenden Unterlagen beschrieben:

1. **Prozessbeschreibung erstellen:** Prozesszweck und Akteure zusammenfassen sowie Startereignis, chronologische Aktivitäten und Endereignis beschreiben. Den sequentiellen Happy Path zugrunde legen und gegebenenfalls Nachrichtenflüsse zwischen Pools klar benennen.
2. **Bestätigung einholen:** Nachfragen, ob auf Grundlage der Beschreibung ein BPMN-Modell erstellt werden soll.
3. **Referenz lesen:** Nach Bestätigung die Datei `BPMN_Template.xml` als verpflichtende technische Grundlage heranziehen.
4. **Modell erzeugen und ablegen:** Die Beschreibung in die XML- und Diagrammstruktur übertragen und im Ordner `CreateBPMN/` unter einem sprechenden, prozessbezogenen Dateinamen speichern, beispielsweise `Personalausweis_beantragen.bpmn`.
5. **Im Zielsystem übernehmen und ergänzen:** Die BPMN-Datei zur weiteren Bearbeitung in Process Studio übernehmen. Erforderliche Zuweisungen, Variablen, Formularreferenzen und gegebenenfalls Serviceanbindungen für die konkrete Umgebung ausgestalten. Ein genauer Importmenüweg ist in der BPMN-Agentenanweisung nicht festgelegt.
6. **Prozess bereitstellen:** Die ergänzende Dokumentation der Beispielprozesse beschreibt die Bereitstellung über die Prozessadministration von d.velop process. Dieser Schritt ist vom Erstellen und Speichern der BPMN-Datei getrennt.
7. **Prozessinstanz starten:** Nach der Beispieldokumentation kann ein bereitgestellter Prozess über die REST-API von d.velop process gestartet werden. Angaben zu URI, HTTP-Headern und Anfrageinhalt werden dort für den bereitgestellten Prozess in der Prozessadministration verortet. Ein automatischer Aufruf durch den BPMN-Agenten ist nicht konfiguriert.

Die erste Ausgabe ist somit eine natürlichsprachliche Prozessbeschreibung. Erst nach Zustimmung ist zusätzlich eine BPMN-Datei vorgesehen. Das im Zielsystem bearbeitete Modell, der bereitgestellte Prozess und eine gestartete Prozessinstanz sind davon zu unterscheidende Bearbeitungs- beziehungsweise Betriebsstände. Eine automatische Synchronisierung zwischen Projektdatei und Zielsystem ist in der Agentenanweisung nicht beschrieben.

Eine automatisierte BPMN-Schemavalidierung, ein protokollierter Testimport oder ein dokumentierter Laufzeittest ist im Workflow des BPMN-Agenten nicht festgelegt. Die herangezogenen Beispiele erläutern technische Strukturen und Nutzungsschritte; ihre Durchführung in einer konkreten Installation wird mit diesem Vermerk nicht nachgewiesen.

## 5. Verantwortung und fachliche Grenzen

Der Agent unterstützt die Erstellung von Prozessentwürfen und deren technische Aufbereitung für Process Studio. Die Feststellung des tatsächlich geltenden Ablaufs, der örtlichen Zuständigkeiten und der fachlichen beziehungsweise rechtlichen Anforderungen bleibt davon zu unterscheiden. Die zuständigen Personen verantworten die fachliche Bestätigung und die Verwendung des Modells im weiteren Prozessmanagement. Ein verbindlicher Freigabe-, Pflege- oder Betriebsprozess ist in der Agentenanweisung nicht festgelegt.

Die Beschränkung auf einen sequentiellen Happy Path bestimmt den vorgesehenen Darstellungsumfang. Ausnahmebehandlungen, parallele Bearbeitungen und weitere Verfahrensvarianten gehören nicht zum regulären Modellierungsauftrag. Das Ergebnis ist deshalb nicht mit einer vollständigen Beschreibung sämtlicher Varianten des Verwaltungsverfahrens gleichzusetzen.

Die technische Ausrichtung auf ausführbare Prozesse unterscheidet diesen Ansatz von einer rein beschreibenden Modellierung. Gleichwohl bewirkt die Erzeugung einer mit `isExecutable="true"` gekennzeichneten Datei noch keine Automatisierung des Verwaltungsverfahrens. Menschliche Aufgaben verbleiben als Benutzeraufgaben; die Anbindung von Fachverfahren erfordert tatsächlich verfügbare Dienste und passende Parameter. Identitäten, Berechtigungen, Formulare, Datenhaltung und Schnittstellen sind für den Betrieb gesondert einzurichten.

Die hinterlegten Konventionen beschreiben die beabsichtigte technische Übergabe. Ein erfolgreicher Import, eine Bereitstellung und die Ausführung in einer bestimmten Process-Studio- beziehungsweise d.velop-process-Installation sind von dieser Konfiguration zu unterscheiden. Der Vermerk hält weder eine fachliche Freigabe noch eine Freigabe zum produktiven Betrieb fest und enthält keine Bewertung der Modellqualität oder der Leistungsfähigkeit des Agenten.

## 6. Quellengrundlage

Grundlage sind die folgenden Projektunterlagen in der zum Dokumentationszeitpunkt eingesehenen Fassung:

- [.github/agents/BPMN_ProcessStudio.agent.md](.github/agents/BPMN_ProcessStudio.agent.md): Agentenkonfiguration, Prozessbeschreibungsregeln, Modellierungsumfang, Bestätigungsschritt, verpflichtende Vorlagenlektüre und Ausgabeort.
- [BPMN_Template.xml](BPMN_Template.xml): ausdrücklich vorgeschriebene Strukturreferenz für Process Studio mit XML-Konventionen, ausführbarem Prozess, Benutzeraufgaben, optionalen Variablen und Serviceaufrufen sowie BPMN-DI.
- [CreateBPMN/Stammdaten_aendern.bpmn](CreateBPMN/Stammdaten_aendern.bpmn): vorhandenes Dateibeispiel für einen sequentiellen Prozess mit sieben Benutzeraufgaben, Zuweisungen und Diagramminformationen; kein Nachweis eines Import- oder Ausführungslaufs.
- [example-bpmn-processes/README.md](example-bpmn-processes/README.md): ergänzende Hinweise zur Bereitstellung über die Prozessadministration und zum Start über die REST-API von d.velop process.
- [example-bpmn-processes/Sync Service/SyncServiceProcess.bpmn](example-bpmn-processes/Sync%20Service/SyncServiceProcess.bpmn): ergänzendes Beispiel für Serviceeigenschaften, einen synchronen Dienstaufruf und die Übergabe von Ein- und Ausgabeparametern.
- [.github/agents/Form_ProcessStudio.agent.md](.github/agents/Form_ProcessStudio.agent.md): ergänzende Konfiguration des gesonderten Formularagenten zur JSON-Ausgabe und Verknüpfung über `camunda:formKey`.
- [TECHNISCHE_DOKUMENTATION.md](TECHNISCHE_DOKUMENTATION.md): technische Voraussetzungen, Modellauswahl und Nutzung über Copilot Chat; die dort beschriebene Camunda-Editor-Nutzung betrifft die Projektumgebung und ist von der Bereitstellung in d.velop process zu unterscheiden.
- [README.md](README.md): Projektkontext der KI-gestützten Prozessmodellierung und des allgemeinen KOI-Ansatzes.

Der Aufbau orientiert sich an der bereitgestellten Vorlage „Aktenvermerk: Technische und fachliche Umsetzung des Agenten ADONIS KOI“. Aussagen zur Process-Studio-Ausrichtung, zu Formularverknüpfungen sowie zur Bereitstellung und zum Prozessstart beruhen auf den genannten Projektunterlagen. Eine eigenständige Herstellerprüfung oder ein Nachweis durch einen konkreten Import- oder Ausführungslauf ist nicht Bestandteil dieses Vermerks.