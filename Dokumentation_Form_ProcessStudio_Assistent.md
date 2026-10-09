# Aktenvermerk: Technische und fachliche Umsetzung des Agenten Form Process Studio

**Themenfeld:** Prozessmanagement und künstliche Intelligenz  
**Dokumentationsstand:** 09.10.2026  
**Gegenstand:** Erstellung von Formularen für das Zielsystem d.velop Process Studio und deren Verknüpfung mit BPMN-Benutzeraufgaben durch den Custom Agent Form_ProcessStudio in Visual Studio Code mit GitHub Copilot

## 1. Anlass und Zielsetzung

Der Agent Form Process Studio unterstützt im Projekt GovModeler die Erstellung digitaler Formulare für die Bearbeitung von Prozessaufgaben in d.velop Process Studio. Ausgehend von Angaben zu Formularzweck, benötigten Feldern und einer zugehörigen BPMN-Aktivität soll der Agent eine Formularbeschreibung im JSON-Format erzeugen und die Referenz auf dieses Formular in die betreffende Benutzeraufgabe des Prozessmodells eintragen.

Der Bezug zum Prozessmanagement besteht in der Verbindung von modelliertem Ablauf und aufgabenbezogener Datenerfassung. Das BPMN-Modell beschreibt die Reihenfolge und Zuständigkeit von Tätigkeiten; das zugeordnete Formular strukturiert die Informationen, die bei einer Tätigkeit angezeigt, erfasst oder ergänzt werden sollen. Die generative KI übernimmt die Übertragung fachlicher Anforderungen in eine technische Formularstruktur sowie die Anpassung der Formularreferenz im BPMN-XML.

Die Ausrichtung auf Process Studio erfolgt durch eine projektspezifische Formularvorlage auf Grundlage von Form.io, einen JSON-Rahmen nach den im Projekt beschriebenen Vorgaben der d.velop Forms API und die Verknüpfung über das Attribut `camunda:formKey`. Ziel ist die Bereitstellung zusammengehöriger Formular- und Prozessdateien für die weitere Übernahme in das Zielsystem.

Der Agent arbeitet dateibasiert in der Projektumgebung. Die tatsächliche Übernahme des Formulars, die Bereitstellung des Prozesses und die Bearbeitung einer Prozessinstanz sind davon getrennt. Dieser Vermerk beschreibt die hinterlegte Konfiguration, die Referenzunterlagen und den vorgesehenen Bearbeitungsablauf. Eine Bewertung oder Evaluation des Agenten ist nicht Gegenstand. Ein konkreter Generierungs-, Import- oder Nutzungslauf wird damit nicht dokumentiert.

## 2. Fachliche Umsetzung und Wissensbasis

Ausgangspunkt sind Anforderungen an ein Formular für eine bestimmte Prozessaufgabe. Die Agentenanweisung nennt folgende Pflichtangaben:

- **Formularname:** eindeutige, beschreibende Bezeichnung, beispielsweise „Antrag prüfen“.
- **Zweck:** Beschreibung des Formularzwecks und seines fachlichen Kontexts.
- **Felder:** Liste der benötigten Formularfelder einschließlich Datentypen.
- **BPMN-Referenz:** Pfad zur Prozessdatei und Kennung der zugehörigen Benutzeraufgabe.

Ergänzend können Validierungsregeln, Layoutwünsche, bedingte Felder und Berechnungen vorgegeben werden. Fehlt ein ausdrücklicher BPMN-Dateipfad, sieht die Anweisung die Suche nach einer passenden Datei im Arbeitsbereich vor. Vor der Formularerstellung soll der Agent die betreffende Benutzeraufgabe identifizieren und ihre Existenz prüfen.

Bei der Ausarbeitung sollen logische Feldgruppen gebildet und schreibgeschützte Kontextinformationen von editierbaren Eingaben unterschieden werden. Beispielsweise können vorhandene Antragsdaten angezeigt werden, während eine Prüfentscheidung und eine Anmerkung neu erfasst werden. Die Anweisung nennt unter anderem Antragsverfahren, Datenerfassungsformulare, Startformulare und Entscheidungsformulare als Anwendungsfälle. Der konkret beschriebene Verknüpfungsworkflow bezieht sich jedoch auf Benutzeraufgaben im BPMN-Modell; ein gesonderter technischer Mechanismus zur Zuordnung eines Startformulars ist dort nicht ausgearbeitet.

Die maßgeblichen Informationsquellen haben unterschiedliche Funktionen:

- **Agentenanweisung:** Rolle, erforderliche Eingaben, Formularerstellung, verbindliche BPMN-Verknüpfung, Werkzeugverwendung, Prüfschritte und Ausgabeorte.
- **Anforderungen der anfragenden Person:** fachlicher Zweck, benötigte Daten, Eingaberegeln und Bezug zur Prozessaufgabe.
- **Formularvorlage:** technische Grundstruktur, Komponenten, Layout, Validierung, bedingte Anzeige und Namenskonventionen.
- **BPMN-Datei:** konkrete Benutzeraufgabe, Aufgaben-ID und vorhandene Attribute als Bezugspunkt der Verknüpfung.
- **Vorhandene Formulardateien:** ergänzende Beispiele für die dateibasierte Formularstruktur.
- **BPMN-Vorlage und technische Projektdokumentation:** Einordnung der Prozessintegration und der Nutzung über Copilot Chat.

Die Agentenanweisung verlangt ausdrücklich, zunächst die vollständige Datei `Form.Template.md` zu lesen. Der Ordner `BeispielForms/` wird ergänzend als Quelle für Formularbeispiele genannt. Eine verbindliche verfahrensspezifische oder rechtliche Wissensquelle ist in der Konfiguration nicht festgelegt. Die Auswahl von Datenfeldern und Pflichtangaben ist daher von einer fachlich und rechtlich bestätigten Festlegung des Erhebungsumfangs zu unterscheiden.

## 3. Technische Umsetzung für das Zielsystem Process Studio

### 3.1 Agentenkonfiguration und Systemgrenze

Form_ProcessStudio ist als Custom Agent in Visual Studio Code mit GitHub Copilot konfiguriert. Die Agentendatei besteht aus einem YAML-Kopf mit Einsatzbeschreibung und Werkzeugauswahl sowie einem natürlichsprachlichen Anweisungstext. Als Einsatzbeschreibung ist die Erstellung von Formularen für d.velop Process Studio und deren Verknüpfung mit BPMN-Aktivitäten hinterlegt.

Die Werkzeugauswahl umfasst Dateierstellung, gezielte Dateibearbeitung, Lesen, Suche, Terminalausführung und Zugriff auf Terminalinformationen. Für Änderungen vorhandener BPMN-Dateien verlangt die Anweisung ausdrücklich die vorgesehenen Ersetzungswerkzeuge; eine Bearbeitung über PowerShell oder andere Terminalbefehle soll hierfür nicht erfolgen. Ein spezielles Werkzeug zur direkten Bedienung von Process Studio oder eine vorkonfigurierte Verbindung zur d.velop Forms API ist nicht enthalten.

Die Umsetzung verbindet das Sprachmodell zur Interpretation und Generierung mit der Agentenanweisung und den dateibasierten Referenzen. Die nachfolgend beschriebenen Regeln und Prüfungen sind als Anweisungen formuliert. Ein gesonderter programmatischer Formulargenerator oder Validator ist in der Agentendatei nicht implementiert. Ein eigenes Training auf den Projektunterlagen, eine separate Vektordatenbank oder eine eigenständig implementierte Retrieval-Pipeline sind in den herangezogenen Unterlagen nicht beschrieben.

Ein bestimmtes KI-Modell oder eine Modellversion ist in der Agentendatei nicht festgelegt. Die technische Projektdokumentation sieht die Modellauswahl in Copilot Chat vor. Die konkrete Zielinstallation, Hosting, Speicherung von Eingaben und betriebliche Datenschutzregelungen sind in der Agentenanweisung nicht beschrieben; hierzu trifft dieser Vermerk keine weitergehenden Feststellungen.

### 3.2 JSON-Austauschformat und d.velop-spezifischer Rahmen

Das technische Formularergebnis ist eine Datei mit der Endung `.json`. Die Vorlage unterscheidet zwischen einem äußeren Datensatz und der darin eingebetteten Formularbeschreibung. Der äußere Datensatz enthält folgende Bestandteile:

| Eigenschaft | Bedeutung nach der Vorlage |
|---|---|
| `id` | eindeutige Formular-ID im UUID-Format |
| `name` | Formularname |
| `author`, `lastEditor` | Kennungen für Autor und zuletzt bearbeitende Person |
| `creationDate`, `lastModificationDate` | Zeitangaben im ISO-8601-Format |
| `definition` | als JSON-Zeichenkette eingebettete Formularbeschreibung |
| `_links` | relative Verweise auf Bearbeitungsansicht, API-Ressource und Formularansicht |

Die unter `_links` beschriebenen Pfade folgen den Mustern `/dforms/ui/forms/[id]/edit`, `/dforms/api/forms/[id]` und `/dforms/ui/forms/[id]/view`. Damit ist die Datei auf die im Projekt dokumentierte d.velop-Formularstruktur ausgerichtet. Das Eintragen dieser Pfade führt jedoch keinen API-Aufruf aus und erzeugt keine Ressource im Zielsystem. Ebenso belegen in der Datei enthaltene Autorenkennungen und Zeitangaben keinen im Zielsystem protokollierten Bearbeitungsvorgang.

Technisch wesentlich ist die Eigenschaft `definition`: Sie enthält nicht unmittelbar ein verschachteltes JSON-Objekt, sondern eine Zeichenkette, die ihrerseits JSON beschreibt. Die innere Struktur besteht aus `formioFormDefinition` mit `display: "form"` und einem `components`-Array sowie den Eigenschaften `customCss` und `dvfDefVersion`. Für `dvfDefVersion` ist der Wert `"1.0"` vorgesehen. Anführungszeichen und gegebenenfalls Backslashes der inneren Definition müssen beim Einbetten in die äußere JSON-Datei entsprechend maskiert werden.

Die vorhandene Datei „Antrag prüfen“ veranschaulicht den äußeren Metadatenrahmen und die als Zeichenkette eingebettete Form.io-Definition. Ihr Vorhandensein ist kein Nachweis, dass das Formular bereits in Process Studio importiert oder in einem Prozess verwendet wurde.

### 3.3 Komponenten, Feldkennungen und Layout

Die Formularbeschreibung verwendet Form.io-Komponenten. Die Vorlage beschreibt 16 Komponententypen: `textfield`, `textarea`, `number`, `email`, `phoneNumber`, `checkbox`, `select`, `selectboxes`, `radio`, `button`, `datetime`, `day`, `time`, `currency`, `panel` und `columns`. Diese Aufzählung dokumentiert den Umfang der Projektvorlage, nicht eine unabhängig geprüfte vollständige Komponentenliste des Herstellers.

Eingabefelder werden unter anderem durch `type`, `key`, `label` und `input: true` beschrieben. Der `key` dient als technische Feldkennung und als Bezugspunkt für Bedingungen oder Berechnungen. Sichtbare Beschriftungen stehen in `label`; dort sind Umlaute zulässig. Für technische Schlüssel verlangt die Anweisung eindeutige, sprechende Namen ohne Leerzeichen oder Umlaute und nennt camelCase sowie ergänzende Gruppenpräfixe. Punkte sollen vermieden werden, weil sie nach der Vorlage als Objektpfade interpretiert werden.

Zusammengehörige Felder werden in `panel`-Komponenten gruppiert. `columns` bildet mehrspaltige Anordnungen mit verschachtelten Komponenten ab. Beide dienen der Strukturierung und werden mit `input: false` beschrieben. Das Layout orientiert sich am in der Vorlage erläuterten Zwölf-Spalten-Raster; die Spaltenbreiten sollen zusammen zwölf ergeben, beispielsweise sechs plus sechs für zwei gleich breite Spalten. Einklappbare Bereiche sind für optionale Informationen vorgesehen.

Die Agentenanweisung nennt als Gestaltungsrahmen höchstens 20 bis 25 Felder pro Formular sowie fünf bis sieben Felder pro Panel. Platzhalter, Hilfetexte, Tooltips und eine logische Tab-Reihenfolge sollen die Eingabe unterstützen. Diese Angaben sind Vorgaben für den Formularentwurf, keine nachgewiesenen technischen Grenzen einer konkreten Process-Studio-Installation.

### 3.4 Validierung, bedingte Anzeige und Berechnungen

Eingaberegeln werden innerhalb der jeweiligen Komponente über `validate` beschrieben. Die Vorlage enthält unter anderem `required` für Pflichtfelder, `minLength` und `maxLength` für Textlängen, `min` und `max` für Zahlen sowie `pattern` für reguläre Ausdrücke. Benutzerdefinierte Meldungen können über `customMessage` hinterlegt werden. Reguläre Ausdrücke sollen nach der Anweisung mit `^` und `$` auf die vollständige Eingabe bezogen werden. Eine benutzerdefinierte Validierung über JavaScript wird ebenfalls als Möglichkeit gezeigt.

Für die bedingte Anzeige sieht die Anweisung einfache `conditional`-Objekte mit `show`, `when` und `eq` vor. Ein Feld wird beispielsweise angezeigt, wenn ein anderes Feld einen bestimmten Auswahlwert enthält. Für komplexere Bedingungen nennt sie JSON Logic; die Vorlage enthält zusätzlich ein Muster für `customConditional` mit JavaScript.

Berechnete Werte können über `calculateValue` beschrieben werden, etwa zur Addition von Kostenfeldern. Mit `disabled: true` können vorhandene oder berechnete Informationen als nicht editierbare Kontextdaten dargestellt werden. Die Formularvorlage enthält außerdem Eigenschaften wie `defaultValue`, `hidden` und `clearOnHide`, die das Verhalten einzelner Felder beschreiben.

Eine Schaltfläche mit `action: "submit"` ist in der Prüfliste vorgesehen. Attribute wie `disableOnInvalid` beschreiben das Verhalten bei ungültigen Eingaben. Die Erzeugung solcher Feldregeln ist von ihrer tatsächlichen Verarbeitung im Zielsystem zu unterscheiden. Pflichtfeld- und Formatregeln ersetzen keine fachliche Sachverhaltsprüfung; ein regulärer Ausdruck für eine IBAN stellt beispielsweise allein keine Prüfung ihrer Prüfziffer dar.

Bedingte Formularfelder sind zudem keine BPMN-Verzweigungen. Eine im Formular erfasste Entscheidung ändert nicht allein durch ihr Vorhandensein den Prozessablauf. Soll sie den weiteren Ablauf steuern, müssen die entsprechende Datenübergabe und die Prozesslogik gesondert aufeinander abgestimmt sein.

### 3.5 Bezug zu Prozessdaten

Die Agentenanweisung unterscheidet schreibgeschützte Informationen aus Prozessvariablen von neu zu erfassenden Eingaben. Ein Beispiel beschreibt die Vorbelegung eines Feldes über `calculateValue` mit einem Zugriff auf `data.processVariables?.personalnummer`. Weitere Beispiele verwenden Werte anderer Formularfelder für Berechnungen.

Diese Muster beschreiben die beabsichtigte Nutzung von Daten im Formular. Sie richten jedoch weder Prozessvariablen noch eine Schnittstelle zur Datenübergabe ein. Insbesondere definiert ein Formularschlüssel nicht automatisch eine Prozessvariable. Die Bereitstellung vorhandener Daten, die Zuordnung der Feldschlüssel zu Prozessdaten und die Übernahme abgesendeter Werte sind für die konkrete Umgebung zu klären. Der Vermerk dokumentiert keinen nachgewiesenen Datenaustausch zwischen einer Prozessinstanz und einem Formular.

### 3.6 Verknüpfung mit BPMN-Benutzeraufgaben

Die Verbindung zum Prozessmodell ist ein verpflichtender Bestandteil der Agentenanweisung. Der Agent soll eine eindeutige Formular-ID erzeugen, sie in der JSON-Datei als `id` verwenden und dieselbe Kennung im Attribut `camunda:formKey` der zugehörigen `<userTask>` eintragen. Dafür muss das BPMN-Dokument den Camunda-Namensraum `http://camunda.org/schema/1.0/bpmn` enthalten.

Vor der Änderung soll der Agent die Aufgaben-ID und vorhandene Attribute, etwa Zuweisung und Priorität, lesen. Existiert bereits ein `camunda:formKey`, sieht die Anweisung dessen Aktualisierung vor. Die Änderung erfolgt an der vorhandenen BPMN-Datei; der Formularagent erzeugt dadurch keinen neuen Prozessablauf. Die BPMN-Vorlage des Projekts führt `camunda:formKey` entsprechend als optionale Formularreferenz für Benutzeraufgaben auf.

Als zusammengehörige Ergebnisse sind eine JSON-Datei im Ordner `CreateForm/` und eine aktualisierte BPMN-Datei vorgesehen. Die Abschlussmeldung soll Formularpfad, Formular-ID, zugehörige Benutzeraufgabe und Verknüpfungsstatus nennen. Ein Formular ohne BPMN-Verknüpfung gilt nach der Agentenanweisung als unvollständiges Ergebnis.

Für den Fall einer fehlgeschlagenen BPMN-Aktualisierung verlangt die Anweisung eine Fehlermeldung, die Beibehaltung der Formulardatei und die Ausgabe der Formular-ID mit Hinweisen zur manuellen Verknüpfung. Die beiden Dateischritte sind damit als aufeinanderfolgender Workflow beschrieben; eine technisch abgesicherte Transaktion mit automatischem Zurücksetzen beider Dateien ist nicht implementiert.

### 3.7 Übernahme und Weiterbearbeitung in Process Studio

Die Agentenanweisung beschreibt die Übernahme der aktualisierten BPMN-Datei in d.velop Process Studio und den Import des Formular-JSON über die Forms-Schnittstelle. Sie führt aus, dass das Zielsystem die Formular-ID erkennt und die Verknüpfung nach der Übernahme aktiv ist. Anschließend ist eine Prüfung im Preview-Modus vorgesehen.

Diese Angaben sind Nutzungshinweise aus der Projektkonfiguration. Die Agentendatei enthält keinen direkten Upload, keine hinterlegte Zieladresse und keine Authentifizierung für die Forms-Schnittstelle. Die relative API-Adresse im JSON-Datensatz ersetzt diese Verbindung nicht. Für die tatsächliche Zuordnung müssen insbesondere die im Zielsystem verfügbare Formular-ID und die BPMN-Referenz übereinstimmen; gegebenenfalls beim Import veränderte Kennungen sind dabei zu berücksichtigen.

Die Konfiguration nennt als Versionsbezüge die Template-Version 1.0, `dvfDefVersion: "1.0"`, Form.io 4.x+, d.velop Process Studio 2023+, BPMN 2.0 und Camunda Extension 1.0. Diese Angaben beschreiben die hinterlegte Zielausrichtung. Eine Kompatibilität mit einer bestimmten Installation oder sämtlichen späteren Produktversionen ist durch diesen Vermerk nicht nachgewiesen.

## 4. Bearbeitungsablauf und Ausgabe

Die Interaktion erfolgt über Copilot Chat in Visual Studio Code. Für Form_ProcessStudio ist folgender Ablauf hinterlegt:

1. **Anforderungen aufnehmen:** Formularname, Zweck, Felder und BPMN-Bezug erfassen; ergänzende Regeln zu Layout, Validierung, Bedingungen und Berechnungen berücksichtigen.
2. **Referenz und Prozesskontext lesen:** Die vollständige Formularvorlage heranziehen, die BPMN-Datei ermitteln und die zugehörige Benutzeraufgabe einschließlich ihrer ID und Attribute prüfen.
3. **Formular entwerfen:** Feldtypen auswählen, Informationen gruppieren, Eingaben von Kontextdaten unterscheiden und die erforderlichen Regeln formulieren.
4. **Kennung und Datei erzeugen:** Eine Formular-ID generieren und das Formular unter einem sprechenden Namen im Ordner `CreateForm/` speichern, beispielsweise `Antrag_pruefen.json`.
5. **BPMN-Datei aktualisieren:** Die Formular-ID als `camunda:formKey` in die zugehörige Benutzeraufgabe eintragen oder eine vorhandene Referenz aktualisieren.
6. **Vorgesehene Prüfungen durchführen:** Eindeutigkeit der Schlüssel, Eingabeeigenschaften, Pflichtfeldregeln, Spaltenbreiten, Bedingungsreferenzen, reguläre Ausdrücke, Submit-Schaltfläche, JSON-Syntax und Definitionsversion prüfen. Zusätzlich die XML-Syntax und die Übereinstimmung der Formular-ID mit der BPMN-Referenz prüfen.
7. **Ergebnis mitteilen:** Dateipfad, Formular-ID, BPMN-Aufgabe und Status der Verknüpfung ausgeben; bei einer fehlgeschlagenen Verknüpfung den vorgesehenen Fehlerhinweis geben.
8. **Im Zielsystem übernehmen:** Aktualisierte BPMN-Datei und Formular-JSON über die vorgesehenen Funktionen übernehmen und das Formular im Preview-Modus prüfen. Dieser Schritt ist ein anschließender Nutzungshinweis, kein konfigurierter direkter Zugriff des Agenten auf Process Studio.

Anders als beim BPMN-Agenten ist ein vorgelagerter Bestätigungsschritt zwischen einer natürlichsprachlichen Beschreibung und der Dateierstellung nicht ausdrücklich festgelegt. Die reguläre Ausgabe umfasst das Formular und die Änderung der vorhandenen Prozessdatei.

Die Prüflisten sind Bestandteil der Agentenanweisung und der Vorlage. Eine eigenständig implementierte automatisierte Prüfung oder die protokollierte Durchführung dieser Prüfungen wird damit nicht nachgewiesen. Auch Vorschau, Datenübergabe und Bearbeitung im laufenden Prozess sind von der Erstellung der Dateien getrennte Schritte. Eine automatische Synchronisierung zwischen Projektdateien und Zielsystem ist nicht beschrieben.

## 5. Verantwortung und fachliche Grenzen

Der Agent unterstützt die technische Ausarbeitung von Formularentwürfen und ihre Zuordnung zu Prozessaufgaben. Welche Informationen erhoben werden dürfen und müssen, welche Eingaben verpflichtend sind und welche Entscheidungen damit vorbereitet werden, bleibt fachlich und rechtlich festzulegen. Die zuständigen Personen verantworten die Bestätigung der Inhalte und deren Verwendung im weiteren Prozessmanagement. Ein verbindlicher Freigabe-, Pflege- oder Betriebsprozess ist in der Agentenanweisung nicht festgelegt.

Die Kennzeichnung eines Feldes als schreibgeschützt oder verborgen ist eine Vorgabe für die Formularoberfläche und ersetzt keine Berechtigungsprüfung im Zielsystem. Ebenso bewirken die im Vorlagenumfang enthaltenen Eigenschaften zu Speicherung, Schutz oder Verschlüsselung für sich genommen keinen nachgewiesenen Datenschutz oder eine eingerichtete Zugriffskontrolle. Datenhaltung, Zugriffsrechte und die sichere Verarbeitung von Formularwerten sind gesondert zu regeln.

Die Verknüpfung über `camunda:formKey` ordnet ein Formular einer Benutzeraufgabe zu. Sie stellt weder einen Fachverfahrensanschluss her noch automatisiert sie die fachliche Entscheidung. Die tatsächlich verfügbaren Prozessdaten, die Übernahme von Eingaben und die gegebenenfalls anschließende Ablaufsteuerung müssen mit dem Prozessmodell und der Zielumgebung abgestimmt sein.

Die hinterlegten Format- und Importvorgaben beschreiben die beabsichtigte technische Übergabe an Process Studio. Ein erfolgreicher Import, eine funktionsfähige Formularreferenz und die Bearbeitung innerhalb einer konkreten Prozessinstanz sind von dieser Konfiguration zu unterscheiden. Der Vermerk hält weder eine fachliche Freigabe noch eine Freigabe zum produktiven Betrieb fest und enthält keine Bewertung der Formularqualität oder der Leistungsfähigkeit des Agenten.

## 6. Quellengrundlage

Grundlage sind die folgenden Projektunterlagen in der zum Dokumentationszeitpunkt eingesehenen Fassung:

- [.github/agents/Form_ProcessStudio.agent.md](.github/agents/Form_ProcessStudio.agent.md): Agentenkonfiguration, Eingaben, verpflichtende Vorlagenlektüre, Formularerstellung, BPMN-Verknüpfung, Prüfschritte, Fehlerbehandlung, Importhinweise und Versionsbezüge.
- [Form.Template.md](Form.Template.md): technische Referenz für den JSON-Rahmen, die eingebettete Form.io-Definition, Komponenten, Layout, Validierung, bedingte Anzeige und Namenskonventionen.
- [CreateForm/Antrag_pruefen.json](CreateForm/Antrag_pruefen.json): vorhandenes Dateibeispiel für Formularmetadaten, eine als Zeichenkette eingebettete Definition sowie gruppierte und nicht editierbare Kontextfelder; kein Nachweis eines Import- oder Nutzungslaufs.
- [CreateBPMN/Stammdaten_aendern.bpmn](CreateBPMN/Stammdaten_aendern.bpmn): vorhandener Prozess mit der Benutzeraufgabe `task_antrag_pruefen` als Bezugspunkt des in der Agentenanweisung erläuterten Verknüpfungsbeispiels; kein Nachweis einer tatsächlich eingerichteten Formularanbindung.
- [BPMN_Template.xml](BPMN_Template.xml): ergänzende Prozessvorlage mit Camunda-Namensraum und optionalem Attribut `camunda:formKey` an Benutzeraufgaben.
- [TECHNISCHE_DOKUMENTATION.md](TECHNISCHE_DOKUMENTATION.md): technische Projektumgebung und Nutzung der Formularerstellung über Copilot Chat; die dort genannte Camunda-Forms-Editor-Nutzung ist von dem hier dokumentierten d.velop-spezifischen JSON-Format zu unterscheiden.
- [README.md](README.md): Projektkontext der KI-gestützten Prozessmodellierung und Integration von Formularen.

Der Aufbau orientiert sich an der bereitgestellten Vorlage „Aktenvermerk: Technische und fachliche Umsetzung des Agenten ADONIS KOI“ und dem Aktenvermerk zum Agenten BPMN Process Studio. Aussagen zum Formularformat, zur Verknüpfung und zur Übernahme in das Zielsystem beruhen auf den genannten Projektunterlagen. Eine eigenständige Herstellerprüfung oder ein Nachweis durch einen konkreten Import- oder Nutzungslauf ist nicht Bestandteil dieses Vermerks.