# Aktenvermerk: Technische und fachliche Umsetzung des Agenten Forms

**Themenfeld:** Prozessmanagement und künstliche Intelligenz  
**Dokumentationsstand:** 09.10.2026  
**Gegenstand:** Erstellung von Camunda Forms durch den Custom Agent Forms in Visual Studio Code mit GitHub Copilot

## 1. Anlass und Zielsetzung

Der Agent Forms unterstützt im Projekt GovModeler die Erstellung von Formularen für menschlich bearbeitete Aufgaben in BPMN-Prozessen, sogenannte User Tasks. Er überführt Beschreibungen eines Prozessschritts und seiner Datenerfordernisse in eine strukturierte Formulardatei. Als Anwendungsfälle nennt die Agentenanweisung insbesondere Antragsverfahren, Datenerfassung und Stammdatenänderungen sowie die Erweiterung oder Anpassung bestehender Formulare.

Der Bezug zum Prozessmanagement besteht in der Verbindung von Prozessmodell und Datenerfassung: Das BPMN-Modell beschreibt den Ablauf und die zu bearbeitende Aufgabe; das zugehörige Formular legt fest, welche Angaben Benutzerinnen und Benutzer für diese Aufgabe erfassen sollen. Die KI unterstützt die Übersetzung natürlichsprachlicher Anforderungen in Formularfelder, Eingaberegeln und eine technische JSON-Struktur. Sie führt den Verwaltungsprozess nicht selbst aus und trifft keine fachliche Entscheidung über einen Antrag.

Ziel ist die Bereitstellung einer bearbeitbaren Camunda-Formulardatei als Grundlage für die weitere fachliche und technische Umsetzung. Dieser Vermerk beschreibt die hinterlegte Konfiguration, die verwendeten Projektunterlagen und den vorgesehenen Bearbeitungsablauf. Eine Bewertung oder Evaluation des Agenten ist nicht Gegenstand.

## 2. Fachliche Umsetzung und Wissensbasis

Ausgangspunkt sind der Name der User Task beziehungsweise des Prozessschritts und eine Beschreibung des Formularzwecks. Ergänzend können die benötigten Formularfelder und Validierungsregeln vorgegeben werden. Das zugehörige BPMN-Modell dient dazu, die Aufgabe im Prozess zu identifizieren und das Formular diesem Bearbeitungsschritt zuzuordnen.

Die Agentenanweisung sieht vor, vorhandene Formulare im Ordner CreateForm als Referenz heranzuziehen. Diese Dateien enthalten Beispiele für Feldbezeichnungen, Datenschlüssel, Eingabekomponenten, Validierung und Anordnung. Sie dienen als technische und strukturelle Vorlagen; daraus folgt keine eigenständige fachliche oder rechtliche Verbindlichkeit ihrer Inhalte für andere Verfahren.

Die für Forms maßgeblichen Informationsquellen haben unterschiedliche Funktionen:

- **Agentenanweisung:** Zweck, Eingaben, Ausgabeformat, Komponenten, Namenskonventionen, Arbeitsschritte und Grenzen.
- **BPMN-Prozessmodell:** Zuordnung des Formulars zu einer konkreten User Task und deren Prozesskontext.
- **Formularanforderungen der anfragenden Person:** fachlicher Zweck, benötigte Daten und gegebenenfalls besondere Eingaberegeln.
- **Vorhandene Formulardateien:** Referenzen für die Ausgestaltung der JSON-Struktur.
- **Technische Projektdokumentation:** Nutzung über Copilot Chat und benötigte Editor-Erweiterungen.

Die Formularstruktur soll Titel und Hinweise, logische Feldgruppen, Eingabefelder, Validierungsangaben, Layoutinformationen und einen Absende-Button enthalten. Als Standardkomponenten sind unter anderem einzeilige und mehrzeilige Texteingaben, Checkboxen, Mehrfachauswahl und Dropdown-Auswahl vorgesehen. Pflichtfelder, Längenbeschränkungen und reguläre Ausdrücke können Eingabeanforderungen abbilden. Solche Regeln beschreiben die zulässige Form einer Eingabe; sie ersetzen keine fachliche Prüfung des zugrunde liegenden Sachverhalts.

## 3. Technische Umsetzung

Forms ist als Custom Agent in Visual Studio Code mit GitHub Copilot konfiguriert. Die [Agentendatei](.github/agents/Forms.agent.md) besteht aus einem YAML-Kopf mit Einsatzbeschreibung und Werkzeugauswahl sowie einem Anweisungstext. Dieser legt die Erstellung von Camunda Forms im JSON-Format für BPMN-User-Tasks fest.

Die Werkzeugauswahl umfasst das Erstellen von Dateien, das Lesen von Dateien, Suchfunktionen sowie Terminalausführung und den Zugriff auf Terminalausgaben. Die Konfiguration ist damit auf die Verarbeitung von Projektdateien und die Erzeugung von Formularartefakten ausgerichtet. Die verfügbaren Werkzeuge und der beschriebene Ablauf sind Vorgaben der Konfiguration; dieser Vermerk dokumentiert keinen konkreten Ausführungslauf.

Als Ausgabe sind Dateien mit der Endung `.form` im Ordner CreateForm vorgesehen. Die Agentenanweisung nennt Camunda Platform 7.x, die Plattformversion 7.20.0, Schema-Version 9 und den Exporter GitHub-Copilot-GovModeler. Versionsangaben sind außerdem in den jeweiligen Formulardateien enthalten; das herangezogene Büchereiausweis-Beispiel weist die Plattformversion 7.20.0 und Schema-Version 17 aus.

Für Dateinamen sieht die Anweisung das Muster `Prozessname_Antrag.form` vor. Komponenten-IDs sollen die Präfixe `Field_` beziehungsweise `Field_Group_` verwenden; Datenschlüssel werden in camelCase benannt. Layoutangaben zu Zeilen und Spalten beschreiben die Anordnung der Komponenten. Eine ausdrückliche Strukturvorgabe ist, Gruppen ohne `path`-Attribut anzulegen und Eingabefelder über ihre eigenen `key`-Attribute zu binden.

Zur Verknüpfung mit dem Prozess sieht die Agentenanweisung ein `camunda:formKey`-Attribut an der betreffenden BPMN-User-Task vor. Als Referenzmuster nennt sie `embedded:app:forms/Formularname.form`. Die Ablage einer Datei im Projekt und ihre Referenzierung im BPMN-Modell sind dabei von ihrer Bereitstellung in einer Laufzeitumgebung zu unterscheiden. Ein Deployment oder die Ausführung des Prozesses ist nicht als Arbeitsschritt des Agenten beschrieben.

Die technische Projektdokumentation nennt GitHub Copilot und Copilot Chat für die KI-Interaktion, den Camunda Modeler für BPMN-Modelle und den Camunda Forms Editor für Formulare. Die Agentenanweisung sieht vor, die erzeugte Datei im Forms Editor zu öffnen. Ein eigenes Training auf Projektdateien, eine separate Vektordatenbank oder eine eigenständig implementierte Retrieval-Pipeline sind in den herangezogenen Unterlagen nicht beschrieben.

Ein bestimmtes KI-Modell oder eine Modellversion ist in der Forms-Agentendatei nicht festgelegt. Die technische Dokumentation sieht eine Modellauswahl in Copilot Chat vor. Hosting, Speicherung von Eingaben und betriebliche Datenschutzregelungen werden in der Agentendatei nicht beschrieben; hierzu trifft dieser Vermerk keine weitergehenden Feststellungen.

## 4. Bearbeitungsablauf und Ausgabe

Die Interaktion erfolgt über Copilot Chat. Nach der technischen Projektdokumentation wird der Agent Forms ausgewählt und die Aktivität im BPMN-Modell benannt, für die ein Formular erstellt werden soll. Die Agentenanweisung beschreibt folgenden Ablauf:

1. **Analyse:** BPMN-Prozess und Formularanforderungen betrachten und die betreffende User Task identifizieren.
2. **Referenz heranziehen:** Vorhandene Formulare im Ordner CreateForm als Vorlage verwenden.
3. **Formular erstellen:** JSON-Struktur mit Texten, Gruppen, Feldern, Validierung, Layout und Absende-Button erzeugen; Gruppen ohne `path`-Attribut anlegen.
4. **Datei speichern:** Formular mit der Endung `.form` im vorgesehenen Projektordner ablegen.
5. **BPMN verknüpfen:** Formularreferenz über `formKey` an der zugehörigen User Task setzen.
6. **Editor öffnen:** Formulardatei zur Darstellung und weiteren Bearbeitung im Camunda Forms Editor öffnen.

Bei unklaren Feldanforderungen, besonderen Validierungsregeln oder einer nicht identifizierbaren User-Task-ID soll der Agent Rückfragen stellen. Während der Bearbeitung sind Fortschrittsmeldungen zur Analyse, Erstellung, Speicherung und Verknüpfung vorgesehen.

Das wesentliche Ergebnis ist eine Formulardatei, nicht lediglich eine textliche Beschreibung. Das vorhandene Büchereiausweis-Formular veranschaulicht dieses Ausgabeformat mit persönlichen Angaben, Kontaktdaten, Adresse, Auswahl des Ausweistyps, einer Bestätigungs-Checkbox und einem Absende-Button. Dieses Beispiel dient hier ausschließlich der Beschreibung des Dateiaufbaus; eine Prüfung seiner fachlichen Inhalte oder seiner Funktionsfähigkeit ist nicht Gegenstand des Vermerks.

## 5. Verantwortung und fachliche Grenzen

Der Agent unterstützt die Erstellung technischer Formularentwürfe. Die Festlegung, welche Angaben für einen Verwaltungsvorgang erforderlich sind, sowie die fachliche und rechtliche Freigabe verbleiben bei den zuständigen Personen. Dazu gehören insbesondere die Erforderlichkeit personenbezogener Daten, Pflichtfeldregeln, Auswahlmöglichkeiten und Hinweis- oder Einwilligungstexte. Vom Agenten erzeugte Formulierungen begründen für sich genommen keine Rechtsgrundlage für die Datenverarbeitung.

Die Agentenanweisung beschränkt den Funktionsumfang auf Standardkomponenten von Camunda Platform 7.x. Komplexe Geschäftsregeln oder Skripte, die Integration externer Datenquellen und die Implementierung eigener Komponenten sind ausdrücklich nicht vorgesehen. Die Erstellung eines Formulars ist daher von einer vollständigen Fachanwendung mit Datenhaltung, Berechtigungen, Schnittstellen und produktivem Prozessbetrieb abzugrenzen.

Für eine spätere Verwendung sind die fachliche Freigabe, die technische Einbindung und die Bereitstellung in der jeweiligen Umgebung gesondert zu verantworten. Ein verbindlicher Freigabe-, Pflege- oder Betriebsprozess ist in der Forms-Agentenanweisung nicht festgelegt. Der Vermerk dokumentiert die konfigurierte Unterstützung bei der Formularerstellung, nicht eine Freigabe zur produktiven Nutzung.

## 6. Quellengrundlage

Grundlage sind die folgenden Projektunterlagen in der zum Dokumentationszeitpunkt eingesehenen Fassung:

- [.github/agents/Forms.agent.md](.github/agents/Forms.agent.md): Agentenkonfiguration, Eingaben, Formularstruktur, technische Vorgaben, Workflow und Grenzen.
- [TECHNISCHE_DOKUMENTATION.md](TECHNISCHE_DOKUMENTATION.md): technische Voraussetzungen, Editor-Erweiterungen und Nutzung des Agenten über Copilot Chat.
- [README.md](README.md): Projektkontext der KI-gestützten Prozessmodellierung sowie Erstellung und Integration von Formularen.
- [CreateForm/Buechereiausweis_Antrag.form](CreateForm/Buechereiausweis_Antrag.form): exemplarischer Aufbau einer Formulardatei mit Komponenten, Validierungsregeln, Layout und Versionsangaben.
- [CreateBPMN/Buechereiausweis_erstellen.bpmn](CreateBPMN/Buechereiausweis_erstellen.bpmn): exemplarisches Prozessmodell mit User Tasks als Bezug zur Formularerstellung.