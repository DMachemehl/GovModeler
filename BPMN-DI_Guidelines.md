# BPMN-DI Guidelines: Wichtigste Attribute für Diagram Interchange

## Überblick
BPMN-DI (Business Process Model and Notation - Diagram Interchange) definiert die visuellen Aspekte von BPMN-Diagrammen. Diese Guidelines beschreiben die wichtigsten Attribute für konsistente und professionelle BPMN-Darstellungen.

## Namespace-Definitionen

### Erforderliche Namespaces
```xml
xmlns:bpmn="http://www.omg.org/spec/BPMN/20100524/MODEL"
xmlns:bpmndi="http://www.omg.org/spec/BPMN/20100524/DI"
xmlns:dc="http://www.omg.org/spec/DD/20100524/DC"
xmlns:di="http://www.omg.org/spec/DD/20100524/DI"
```

## 1. BPMNDiagram - Diagramm-Container

### Grundlegende Struktur
```xml
<bpmndi:BPMNDiagram id="BPMNDiagram_1">
  <bpmndi:BPMNPlane id="BPMNPlane_1" bpmnElement="Collaboration_ID">
    <!-- Alle visuellen Elemente -->
  </bpmndi:BPMNPlane>
</bpmndi:BPMNDiagram>
```

### Wichtige Attribute
- **id**: Eindeutige Identifikation des Diagramms
- **name** (optional): Benutzerfreundlicher Name des Diagramms

## 2. BPMNPlane - Zeichenebene

### Wichtige Attribute
- **id**: Eindeutige Identifikation der Zeichenebene
- **bpmnElement**: Referenz auf das zugehörige BPMN-Element (meist Collaboration)

## 3. BPMNShape - Visuelle Formen

### Grundstruktur
```xml
<bpmndi:BPMNShape id="Element_di" bpmnElement="Element_ID" isHorizontal="true">
  <dc:Bounds x="160" y="80" width="900" height="250" />
  <bpmndi:BPMNLabel>
    <dc:Bounds x="170" y="200" width="80" height="27" />
  </bpmndi:BPMNLabel>
</bpmndi:BPMNShape>
```

### Wichtige Attribute

#### Identifikation
- **id**: Eindeutige ID für die visuelle Form (Konvention: ElementName_di)
- **bpmnElement**: Referenz auf das zugehörige BPMN-Modellelement

#### Layout-Attribute
- **isHorizontal**: Für Pools und Lanes (true/false)
- **isMarkerVisible**: Für Gateways mit speziellen Markern
- **isExpanded**: Für Sub-Prozesse (true/false)

#### Positionierung (dc:Bounds)
- **x**: X-Koordinate der linken oberen Ecke
- **y**: Y-Koordinate der linken oberen Ecke
- **width**: Breite des Elements
- **height**: Höhe des Elements

### Standard-Dimensionen

#### Pools und Lanes
```xml
<!-- Pool mit erweiterter Breite für horizontale Task-Anordnung -->
<dc:Bounds x="160" y="80" width="1200" height="250" />

<!-- Lane innerhalb Pool -->
<dc:Bounds x="190" y="80" width="1170" height="125" />
```

#### Standard-Aktivitäten (OBLIGATORISCHE horizontale Anordnung)
```xml
<!-- Task 1 - Referenz Y-Koordinate für den Pool -->
<dc:Bounds x="310" y="160" width="100" height="80" />

<!-- Task 2 - EXAKT dieselbe Y-Koordinate -->
<dc:Bounds x="470" y="160" width="100" height="80" />

<!-- Task 3 - EXAKT dieselbe Y-Koordinate -->
<dc:Bounds x="630" y="160" width="100" height="80" />

<!-- Task 4 - EXAKT dieselbe Y-Koordinate -->
<dc:Bounds x="790" y="160" width="100" height="80" />

<!-- Start Event - auf Task-Linie oder leicht versetzt -->
<dc:Bounds x="222" y="182" width="36" height="36" />

<!-- End Event - auf Task-Linie oder leicht versetzt -->
<dc:Bounds x="952" y="182" width="36" height="36" />

<!-- Intermediate Events - auf Task-Linie -->
<dc:Bounds x="752" y="182" width="36" height="36" />

<!-- Gateway - auf Task-Linie oder minimal versetzt -->
<dc:Bounds x="545" y="175" width="50" height="50" />
```

#### **REGELWERK für horizontale Task-Anordnung:**
- **Y-Koordinate**: Alle Tasks in einem Pool verwenden EXAKT dieselbe Y-Koordinate
- **X-Abstände**: Minimum 160px zwischen Tasks (100px Task-Breite + 60px Abstand)
- **Event-Positionierung**: Start/End Events max. ±22px von Task Y-Koordinate versetzt
- **Gateway-Positionierung**: Gateways max. ±15px von Task Y-Koordinate versetzt
- **Keine Ausnahmen**: Vertikale Task-Versätze sind in KEINEM Fall erlaubt

## 4. BPMNLabel - Textbeschriftungen

### Grundstruktur
```xml
<bpmndi:BPMNLabel>
  <dc:Bounds x="200" y="225" width="80" height="27" />
</bpmndi:BPMNLabel>
```

### Positionierungsregeln
- **Start/End Events**: Label unterhalb des Elements
- **Tasks**: Label in der Mitte des Elements
- **Gateways**: Label oberhalb oder unterhalb
- **Pools**: Label vertikal am linken Rand

### Dimensionsrichtlinien
- **Breite**: 60-120 Pixel je nach Textlänge
- **Höhe**: 14 Pixel pro Textzeile, 27 Pixel für mehrzeiligen Text

## 5. BPMNEdge - Verbindungslinien

### Grundstruktur
```xml
<bpmndi:BPMNEdge id="Flow_ID_di" bpmnElement="Flow_ID">
  <di:waypoint x="258" y="200" />
  <di:waypoint x="310" y="200" />
  <bpmndi:BPMNLabel>
    <dc:Bounds x="270" y="180" width="28" height="14" />
  </bpmndi:BPMNLabel>
</bpmndi:BPMNEdge>
```

### Wichtige Attribute
- **id**: Eindeutige ID (Konvention: FlowName_di)
- **bpmnElement**: Referenz auf Sequence Flow oder Message Flow

### Waypoint-Regeln
- **Minimum**: 2 Waypoints (Start und Ende)
- **Routing**: Zusätzliche Waypoints für Richtungsänderungen
- **Koordinaten**: Exakte Pixel-Positionen

### Routing-Best Practices
```xml
<!-- Gerade Linie -->
<di:waypoint x="258" y="200" />
<di:waypoint x="310" y="200" />

<!-- Mit Richtungsänderung -->
<di:waypoint x="385" y="215" />
<di:waypoint x="385" y="168" />
<di:waypoint x="470" y="168" />
```

### Konnektivität zwischen drei Pools
```xml
<!-- Message Flow zwischen Bürger und Fachanwendung -->
<di:waypoint x="360" y="258" />
<di:waypoint x="360" y="500" />  <!-- Zwischenpunkt beim Fachanwendungs-Pool -->
<di:waypoint x="240" y="500" />
<di:waypoint x="240" y="527" />

<!-- Message Flow zwischen Fachanwendung und Behörde -->
<di:waypoint x="780" y="505" />
<di:waypoint x="780" y="700" />
<di:waypoint x="318" y="700" />
<di:waypoint x="318" y="992" />
```

## 6. Message Flows - Besondere Behandlung

### Styling
```xml
<bpmndi:BPMNEdge id="MsgFlow_Antrag_di" bpmnElement="MsgFlow_Antrag">
  <di:waypoint x="360" y="240" />
  <di:waypoint x="360" y="346" />
  <di:waypoint x="240" y="346" />
  <di:waypoint x="240" y="452" />
  <bpmndi:BPMNLabel>
    <dc:Bounds x="280" y="325" width="80" height="14" />
  </bpmndi:BPMNLabel>
</bpmndi:BPMNEdge>
```

### Besonderheiten
- Gestrichelte Linie (automatisch durch BPMN-Standard)
- Kreuzung zwischen Pools vermeiden
- Label in der Mitte der Verbindung
- Bei drei Pools: Message Flows sollten klare Wege zwischen den Pools nehmen
- Fachanwendungs-Message Flows sollten die kürzeste Route wählen

## 7. Layout-Richtlinien

### Abstände
- **Zwischen Elementen**: Minimum 20 Pixel horizontal, 10 Pixel vertikal
- **Pool-Ränder**: 30-50 Pixel Innenabstand

### **Horizontale Task-Anordnung (OBLIGATORISCH)**
- **Grundregel**: Alle Tasks und Service-Aktivitäten in einem Pool MÜSSEN auf derselben horizontalen Y-Koordinate positioniert werden
- **Keine vertikalen Versätze**: Tasks dürfen niemals vertikal zueinander versetzt angeordnet werden
- **Lineare Sequenz**: Workflow-Elemente folgen einer strikten Links-nach-Rechts-Anordnung
- **Events-Positionierung**: Start-, Intermediate- und End-Events auf derselben Höhe wie Tasks oder leicht versetzt (max. ±22px)
- **Ausnahmen**: Nur Message Flows und Gateways dürfen von der horizontalen Regel abweichen

### Grid-System
- **Raster**: 10-Pixel-Grid empfohlen
- **Ausrichtung**: Alle Koordinaten als Vielfache von 10
- **Y-Koordinaten-Standard**: Tasks in einem Pool verwenden einheitliche Y-Koordinate (z.B. y="160", y="455", y="760")

### Pool-Anordnung
- **Reihenfolge**: Kunde (Bürger) > IT/Fachanwendung > Organisation (Behörde)
- **Abstand zwischen Pools**: 40 Pixel empfohlen
- **Pool-Breite**: Minimum 1200 Pixel für horizontale Task-Anordnung
- **Pool-Höhe**: Maximum 300 Pixel pro Pool (250px Standard + 50px Puffer)
- **Task-Layout innerhalb Pool**: Alle Tasks auf einer horizontalen Ebene, strikt sequentielle Anordnung von links nach rechts

### Größenstandards
```xml
<!-- Standard Task (horizontale Anordnung) -->
width="100" height="80"

<!-- Standard Event (auf Task-Linie) -->  
width="36" height="36"

<!-- Standard Gateway (auf Task-Linie) -->
width="50" height="50"

<!-- Pool für horizontale Tasks (OBLIGATORISCH) -->
width="1200" height="300"

<!-- Pool-Mindesthöhe für horizontale Anordnung -->
height="300"
```

### **Y-Koordinaten-Standards für horizontale Task-Anordnung:**
```xml
<!-- Bürger-Pool (oberster Pool) -->
Tasks: y="160"    Events: y="182"    Gateways: y="175"

<!-- IT/Fachanwendungs-Pool (mittlerer Pool) -->  
Tasks: y="455"    Events: y="477"    Gateways: y="470"

<!-- Behörden-Pool (unterster Pool) -->
Tasks: y="760"    Events: y="782"    Gateways: y="775"
```

### Horizontale Task-Anordnung (Neue Regel)
```xml
<!-- Beispiel: 6 Tasks in horizontaler Linie -->
<!-- Task 1 -->
<dc:Bounds x="310" y="160" width="100" height="80" />
<!-- Task 2 -->
<dc:Bounds x="470" y="160" width="100" height="80" />
<!-- Task 3 -->
<dc:Bounds x="630" y="160" width="100" height="80" />
<!-- Task 4 -->
<dc:Bounds x="790" y="160" width="100" height="80" />
<!-- Task 5 -->
<dc:Bounds x="950" y="160" width="100" height="80" />
<!-- Task 6 -->
<dc:Bounds x="1110" y="160" width="100" height="80" />

<!-- WICHTIG: Alle Tasks haben identische Y-Koordinate (160) -->
<!-- Horizontaler Abstand zwischen Tasks: 160 Pixel (100 + 60 Abstand) -->
```

## 8. Spezielle Elemente

### Event-Based Gateway
```xml
<bpmndi:BPMNShape id="Gateway_Event_di" bpmnElement="Gateway_Event">
  <dc:Bounds x="360" y="215" width="50" height="50" />
  <bpmndi:BPMNLabel>
    <dc:Bounds x="345" y="185" width="80" height="27" />
  </bpmndi:BPMNLabel>
</bpmndi:BPMNShape>
```

### Exclusive Gateway mit Marker
```xml
<bpmndi:BPMNShape id="Gateway_Vollstaendig_di" bpmnElement="Gateway_Vollstaendig" isMarkerVisible="true">
  <dc:Bounds x="485" y="545" width="50" height="50" />
  <bpmndi:BPMNLabel>
    <dc:Bounds x="475" y="515" width="70" height="14" />
  </bpmndi:BPMNLabel>
</bpmndi:BPMNShape>
```

### Task-Typen

#### Standard Task
```xml
<bpmndi:BPMNShape id="Task_Standard_di" bpmnElement="Task_Standard">
  <dc:Bounds x="220" y="530" width="100" height="80" />
</bpmndi:BPMNShape>
```

#### Service Task
```xml
<bpmndi:BPMNShape id="Task_Service_di" bpmnElement="Task_Service">
  <dc:Bounds x="220" y="530" width="100" height="80" />
</bpmndi:BPMNShape>
```

#### User Task
```xml
<bpmndi:BPMNShape id="Task_User_di" bpmnElement="Task_User">
  <dc:Bounds x="220" y="530" width="100" height="80" />
</bpmndi:BPMNShape>
```

#### Manual Task
```xml
<bpmndi:BPMNShape id="Task_Manual_di" bpmnElement="Task_Manual">
  <dc:Bounds x="220" y="530" width="100" height="80" />
</bpmndi:BPMNShape>
```

#### Script Task
```xml
<bpmndi:BPMNShape id="Task_Script_di" bpmnElement="Task_Script">
  <dc:Bounds x="220" y="530" width="100" height="80" />
</bpmndi:BPMNShape>
```

#### Send Task
```xml
<bpmndi:BPMNShape id="Task_Send_di" bpmnElement="Task_Send">
  <dc:Bounds x="220" y="530" width="100" height="80" />
</bpmndi:BPMNShape>
```

#### Receive Task
```xml
<bpmndi:BPMNShape id="Task_Receive_di" bpmnElement="Task_Receive">
  <dc:Bounds x="220" y="530" width="100" height="80" />
</bpmndi:BPMNShape>
```

#### Business Rule Task
```xml
<bpmndi:BPMNShape id="Task_BusinessRule_di" bpmnElement="Task_BusinessRule">
  <dc:Bounds x="220" y="530" width="100" height="80" />
</bpmndi:BPMNShape>
```

### Sub-Prozesse

#### Sub-Process (collapsed)
```xml
<bpmndi:BPMNShape id="SubProcess_Collapsed_di" bpmnElement="SubProcess_Collapsed" isExpanded="false">
  <dc:Bounds x="300" y="160" width="100" height="80" />
</bpmndi:BPMNShape>
```

#### Sub-Process (expanded)
```xml
<bpmndi:BPMNShape id="SubProcess_Expanded_di" bpmnElement="SubProcess_Expanded" isExpanded="true">
  <dc:Bounds x="300" y="160" width="350" height="200" />
</bpmndi:BPMNShape>
```

#### Call Activity
```xml
<bpmndi:BPMNShape id="CallActivity_di" bpmnElement="CallActivity">
  <dc:Bounds x="300" y="160" width="100" height="80" />
</bpmndi:BPMNShape>
```

### Fachanwendungs-Elemente

#### Service Task für Fachanwendungen
```xml
<bpmndi:BPMNShape id="Task_Fachanwendung_Daten_verarbeiten_di" bpmnElement="Task_Fachanwendung_Daten_verarbeiten">
  <dc:Bounds x="310" y="505" width="100" height="80" />
</bpmndi:BPMNShape>
```

#### Fachanwendungs-Gateway
```xml
<bpmndi:BPMNShape id="Gateway_Fachanwendung_Erfolg_di" bpmnElement="Gateway_Fachanwendung_Erfolg" isMarkerVisible="true">
  <dc:Bounds x="465" y="520" width="50" height="50" />
  <bpmndi:BPMNLabel>
    <dc:Bounds x="465" y="470" width="90" height="27" />
  </bpmndi:BPMNLabel>
</bpmndi:BPMNShape>
```

#### Fachanwendungs-Pool
```xml
<bpmndi:BPMNShape id="Participant_Fachanwendung_di" bpmnElement="Participant_Fachanwendung" isHorizontal="true">
  <dc:Bounds x="160" y="420" width="1200" height="250" />
  <bpmndi:BPMNLabel>
    <dc:Bounds x="170" y="530" width="20" height="80" />
  </bpmndi:BPMNLabel>
</bpmndi:BPMNShape>
```

### Event-Typen

#### Start Events
```xml
<!-- None Start Event -->
<bpmndi:BPMNShape id="StartEvent_None_di" bpmnElement="StartEvent_None">
  <dc:Bounds x="222" y="182" width="36" height="36" />
</bpmndi:BPMNShape>

<!-- Message Start Event -->
<bpmndi:BPMNShape id="StartEvent_Message_di" bpmnElement="StartEvent_Message">
  <dc:Bounds x="222" y="182" width="36" height="36" />
</bpmndi:BPMNShape>

<!-- Timer Start Event -->
<bpmndi:BPMNShape id="StartEvent_Timer_di" bpmnElement="StartEvent_Timer">
  <dc:Bounds x="222" y="182" width="36" height="36" />
</bpmndi:BPMNShape>

<!-- Signal Start Event -->
<bpmndi:BPMNShape id="StartEvent_Signal_di" bpmnElement="StartEvent_Signal">
  <dc:Bounds x="222" y="182" width="36" height="36" />
</bpmndi:BPMNShape>
```

#### Intermediate Events
```xml
<!-- Intermediate Catch Event -->
<bpmndi:BPMNShape id="IntermediateCatchEvent_di" bpmnElement="IntermediateCatchEvent">
  <dc:Bounds x="470" y="150" width="36" height="36" />
</bpmndi:BPMNShape>

<!-- Intermediate Throw Event -->
<bpmndi:BPMNShape id="IntermediateThrowEvent_di" bpmnElement="IntermediateThrowEvent">
  <dc:Bounds x="470" y="150" width="36" height="36" />
</bpmndi:BPMNShape>

<!-- Boundary Event -->
<bpmndi:BPMNShape id="BoundaryEvent_di" bpmnElement="BoundaryEvent">
  <dc:Bounds x="352" y="222" width="36" height="36" />
</bpmndi:BPMNShape>
```

#### End Events
```xml
<!-- None End Event -->
<bpmndi:BPMNShape id="EndEvent_None_di" bpmnElement="EndEvent_None">
  <dc:Bounds x="912" y="182" width="36" height="36" />
</bpmndi:BPMNShape>

<!-- Message End Event -->
<bpmndi:BPMNShape id="EndEvent_Message_di" bpmnElement="EndEvent_Message">
  <dc:Bounds x="912" y="182" width="36" height="36" />
</bpmndi:BPMNShape>

<!-- Terminate End Event -->
<bpmndi:BPMNShape id="EndEvent_Terminate_di" bpmnElement="EndEvent_Terminate">
  <dc:Bounds x="912" y="182" width="36" height="36" />
</bpmndi:BPMNShape>

<!-- Error End Event -->
<bpmndi:BPMNShape id="EndEvent_Error_di" bpmnElement="EndEvent_Error">
  <dc:Bounds x="912" y="182" width="36" height="36" />
</bpmndi:BPMNShape>
```

### Gateway-Typen

#### Exclusive Gateway (XOR)
```xml
<bpmndi:BPMNShape id="Gateway_Exclusive_di" bpmnElement="Gateway_Exclusive" isMarkerVisible="true">
  <dc:Bounds x="485" y="545" width="50" height="50" />
</bpmndi:BPMNShape>
```

#### Inclusive Gateway (OR)
```xml
<bpmndi:BPMNShape id="Gateway_Inclusive_di" bpmnElement="Gateway_Inclusive" isMarkerVisible="true">
  <dc:Bounds x="485" y="545" width="50" height="50" />
</bpmndi:BPMNShape>
```

#### Parallel Gateway (AND)
```xml
<bpmndi:BPMNShape id="Gateway_Parallel_di" bpmnElement="Gateway_Parallel">
  <dc:Bounds x="485" y="545" width="50" height="50" />
</bpmndi:BPMNShape>
```

#### Complex Gateway
```xml
<bpmndi:BPMNShape id="Gateway_Complex_di" bpmnElement="Gateway_Complex" isMarkerVisible="true">
  <dc:Bounds x="485" y="545" width="50" height="50" />
</bpmndi:BPMNShape>
```

## 9. Conditional Flows

### Mit Bedingungstext
```xml
<bpmndi:BPMNEdge id="Flow_Gateway_Einkommenspruefung_di" bpmnElement="Flow_Gateway_Einkommenspruefung">
  <di:waypoint x="535" y="570" />
  <di:waypoint x="600" y="570" />
  <bpmndi:BPMNLabel>
    <dc:Bounds x="545" y="552" width="60" height="14" />
  </bpmndi:BPMNLabel>
</bpmndi:BPMNEdge>
```

## 10. Best Practices

### Konsistenz
- Einheitliche Namenskonventionen für IDs
- Gleiche Abstände zwischen ähnlichen Elementen
- Konsistente Label-Positionierung
- **OBLIGATORISCH**: Alle Tasks in einem Pool auf identischer Y-Koordinate

### Lesbarkeit
- Ausreichend Platz für Text-Labels
- Vermeidung von Linienkreuzungen
- **Logischer Fluss von links nach rechts (OBLIGATORISCH)**
- **Horizontale Task-Konsistenz**: Alle Tasks innerhalb eines Pools auf derselben Y-Koordinate
- **Sequentieller Ablauf**: Tasks niemals vertikal stapeln, immer horizontale Verkettung
- **Standardisierte Pool-Breite**: Minimum 1200px für horizontale Task-Anordnung

### Wartbarkeit
- Sprechende Element-IDs
- Modularer Aufbau bei komplexen Diagrammen
- Kommentare bei komplexen Routings
- **Y-Koordinaten-Standards**: Verwendung der standardisierten Y-Koordinaten pro Pool-Typ

### Validierung
- Alle bpmnElement-Referenzen müssen existieren
- Waypoints müssen geometrisch sinnvoll sein
- Labels dürfen nicht überlappen
- **Tasks MÜSSEN auf identischer Y-Koordinate pro Pool positioniert sein**
- **Pool-Breite MUSS mindestens 1200px betragen**

## 16. Horizontale Task-Anordnung (Neue Vorgabe)

### Grundprinzip
Alle Tasks, Service Tasks, User Tasks und andere Aktivitäten innerhalb eines Pools **müssen** auf einer horizontalen Linie positioniert werden. Vertikale Verschiebungen von Tasks sind nicht erlaubt.

### Implementierungsregeln
```xml
<!-- RICHTIG: Alle Tasks auf Y=160 -->
<bpmndi:BPMNShape id="Task1_di" bpmnElement="Task1">
  <dc:Bounds x="310" y="160" width="100" height="80" />
</bpmndi:BPMNShape>
<bpmndi:BPMNShape id="Task2_di" bpmnElement="Task2">
  <dc:Bounds x="470" y="160" width="100" height="80" />
</bpmndi:BPMNShape>
<bpmndi:BPMNShape id="Task3_di" bpmnElement="Task3">
  <dc:Bounds x="630" y="160" width="100" height="80" />
</bpmndi:BPMNShape>

<!-- FALSCH: Tasks auf unterschiedlichen Y-Koordinaten -->
<bpmndi:BPMNShape id="Task1_di" bpmnElement="Task1">
  <dc:Bounds x="310" y="160" width="100" height="80" />
</bpmndi:BPMNShape>
<bpmndi:BPMNShape id="Task2_di" bpmnElement="Task2">
  <dc:Bounds x="470" y="240" width="100" height="80" />  <!-- FALSCH: Y=240 -->
</bpmndi:BPMNShape>
```

### Pool-spezifische Y-Koordinaten
```xml
<!-- Bürger-Pool: Tasks auf Y=160 (Pool-Mitte bei Y=180) -->
<dc:Bounds x="310" y="160" width="100" height="80" />

<!-- IT-Pool: Tasks auf Y=400 (Pool-Mitte bei Y=420) -->
<dc:Bounds x="310" y="400" width="100" height="80" />

<!-- Behörden-Pool: Tasks auf Y=640 (Pool-Mitte bei Y=660) -->
<dc:Bounds x="310" y="640" width="100" height="80" />
```

### Sequence Flow Routing
```xml
<!-- Bei horizontaler Anordnung: Gerade Linien zwischen Tasks -->
<bpmndi:BPMNEdge id="Flow_Task1_Task2_di" bpmnElement="Flow_Task1_Task2">
  <di:waypoint x="410" y="200" />  <!-- Ende Task1 -->
  <di:waypoint x="470" y="200" />  <!-- Start Task2 -->
</bpmndi:BPMNEdge>
```

### Ausnahmen
- **Events**: Können leicht vertikal angepasst werden (±10 Pixel)
- **Gateways**: Sollten ebenfalls auf der Task-Linie bleiben
- **Labels**: Können oberhalb/unterhalb der Task-Linie positioniert werden

### Vorteile
- **Bessere Lesbarkeit**: Klarer sequentieller Ablauf
- **Professionellere Darstellung**: Standardisierte Business-Process-Optik
- **Einfachere Wartung**: Konsistente Koordinaten-Struktur
- **Platzersparnis**: Kompaktere Pools durch horizontale Ausnutzung

## 15. Häufige Fehler vermeiden
```xml
<bpmndi:BPMNShape id="DataObject_di" bpmnElement="DataObject">
  <dc:Bounds x="400" y="300" width="36" height="50" />
  <bpmndi:BPMNLabel>
    <dc:Bounds x="380" y="357" width="76" height="14" />
  </bpmndi:BPMNLabel>
</bpmndi:BPMNShape>
```

### Data Stores
```xml
<bpmndi:BPMNShape id="DataStore_di" bpmnElement="DataStore">
  <dc:Bounds x="400" y="300" width="50" height="50" />
  <bpmndi:BPMNLabel>
    <dc:Bounds x="375" y="357" width="100" height="14" />
  </bpmndi:BPMNLabel>
</bpmndi:BPMNShape>
```

### Text Annotations
```xml
<bpmndi:BPMNShape id="TextAnnotation_di" bpmnElement="TextAnnotation">
  <dc:Bounds x="400" y="80" width="100" height="50" />
</bpmndi:BPMNShape>
```

### Association (Data/Annotation)
```xml
<bpmndi:BPMNEdge id="Association_di" bpmnElement="Association">
  <di:waypoint x="370" y="200" />
  <di:waypoint x="400" y="180" />
</bpmndi:BPMNEdge>
```

### Groups
```xml
<bpmndi:BPMNShape id="Group_di" bpmnElement="Group">
  <dc:Bounds x="300" y="150" width="300" height="200" />
  <bpmndi:BPMNLabel>
    <dc:Bounds x="435" y="160" width="30" height="14" />
  </bpmndi:BPMNLabel>
</bpmndi:BPMNShape>
```

## 13. Spezielle Attribute für Task-Marker

### Mehrere Task-Marker kombinieren
```xml
<!-- User Task mit Loop-Marker -->
<bpmndi:BPMNShape id="Task_UserLoop_di" bpmnElement="Task_UserLoop">
  <dc:Bounds x="220" y="530" width="100" height="80" />
</bpmndi:BPMNShape>

<!-- Service Task mit Multi-Instance Marker -->
<bpmndi:BPMNShape id="Task_ServiceMulti_di" bpmnElement="Task_ServiceMulti">
  <dc:Bounds x="220" y="530" width="100" height="80" />
</bpmndi:BPMNShape>
```

### Boundary Event Positioning
```xml
<!-- An Task-Grenze positioniert -->
<bpmndi:BPMNShape id="BoundaryEvent_Timer_di" bpmnElement="BoundaryEvent_Timer">
  <dc:Bounds x="302" y="222" width="36" height="36" />
</bpmndi:BPMNShape>
```

## 14. Dimensionsstandards Erweitert

### Erweiterte Standard-Dimensionen
```xml
<!-- Große Tasks/Sub-Prozesse -->
width="120" height="80"    <!-- Für längere Labels -->

<!-- Kompakte Tasks -->
width="80" height="60"     <!-- Für einfache Aktionen -->

<!-- Call Activities -->
width="100" height="80"    <!-- Standard wie Tasks -->

<!-- Expanded Sub-Process -->
width="350" height="200"   <!-- Mindestgröße für Inhalt -->

<!-- Data Objects -->
width="36" height="50"     <!-- Standard Datenobjekt -->

<!-- Data Stores -->
width="50" height="50"     <!-- Standard Datenspeicher -->

<!-- Text Annotations -->
width="100" height="50"    <!-- Variable je nach Text -->
```

### Koordinaten-Probleme
- Negative Koordinaten vermeiden
- Realistische Dimensionen verwenden
- Überlappende Elemente prüfen

### Referenz-Fehler
- bpmnElement-IDs müssen im Model existieren
- Eindeutige DI-IDs verwenden
- Korrekte Namespace-Präfixe

### Layout-Probleme
- Ausreichend Platz für Labels einplanen
- Minimum-Abstände einhalten
- Lesbare Diagrammgröße wählen
- **Task-Positionierung**: Niemals Tasks vertikal versetzen - immer horizontale Anordnung verwenden
- **Pool-Breite**: Ausreichende Breite für horizontale Task-Verkettung einplanen (minimum 1200px)

---

**Version**: 1.2  
**Erstellt**: August 2025  
**Aktualisiert**: August 2025  
**Änderungen**: 
- v1.1: Ergänzung für Fachanwendungs-Kollaboration  
- v1.2: Neue Vorgabe für horizontale Task-Anordnung, erweiterte Pool-Breiten, Layout-Standardisierung  
**Für**: GitHub Copilot GovModeler Projekt
