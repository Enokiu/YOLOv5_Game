# YOLOv5 Jump and Run Object Detection Game

## Einleitung
Dieses Projekt zielt darauf ab, ein Objekterkennungsspiel unter Verwendung von Deep Vision zu entwickeln, bei dem der Spieler durch Gesten mit einer geöffneten Hand springt und mit einer Faust läuft. Dies wird durch das Trainieren eines YOLOv5-Modells ermöglicht, das mit einem eigens erstellten Datensatz entwickelt wird.

## Datensatz
Der Datensatz wird durch die Erfassung von Bildern der eigenen Hand erstellt. Insgesamt wurden 200 Bilder mithilfe einer Webcam aufgenommen, die später für die Tests des Spiels verwendet werden. Zur Steigerung der Datenvielfalt werden Augmentierungstechniken angewendet, bei denen jedes Bild um 250 zusätzliche Bilder erweitert wird. Die angewendeten Augmentierungsmethoden umfassen:

- Rotation
- Anpassung von Helligkeit und Kontrast
- Skalierung und Verschiebung
- Hinzufügen von Rauschen
- Horizontale Spiegelung
  
Alle augmentierten Bilder werden in einem einzigen Ordner zusammengeführt.

Da im späteren Verlauf der Entwicklung sich herausstellte, dass der selbst erstellte Datensatz nicht ausreichend war, wurden zusätzlich 500 Bilder generiert. Diese neuen Bilder enthalten sowohl einen Hintergrund als auch eine Person, da das YOLOv5-Modell manchmal den Kopf einer Person als Faust interpretierte. Die Erweiterung umfasst 100 Bilder von geöffneten Händen und 100 Bilder von Fäusten. Zusätzlich wurden 300 Bilder mithilfe von Augmentierungstechniken generiert. Diese Bilder werden manuell gelabelt (unter Verwendung von makesense.ai) und in den vorhandenen Datensatz integriert. Insgesamt enthält der Datensatz nun 950 Bilder.

## Labeling
Die Labels werden mithilfe von makesense.ai erstellt, wobei Bounding Boxes manuell erstellt werden.

**YOLO-Format:**
Im Folgenden ist das YOLO-Format dargestellt: `0 0.603985 0.539020 0.333748 0.494811`. 
- Die erste Spalte enthält die Klassenindizes (0 steht für geöffnete Hand, 1 steht für Faust).
- Die zweite bis fünfte Spalte enthält die normalisierten Koordinaten der Bounding Box (x, y, w, h).

## Aufteilung des Datensatzes im YOLOv5-Format
Um den selbst erstellten Datensatz für das YOLOv5-Training vorzubereiten, wird er in einen 80% Trainingsdatensatz und einen 20% Validierungsdatensatz aufgeteilt. Nach der Aufteilung ist es von entscheidender Bedeutung sicherzustellen, dass ausreichend Bilder für beide Klassen, nämlich "Geöffnete Hand" und "Faust", vorhanden sind. Ein ausgewogenes Verhältnis zwischen den Klassen ist entscheidend für ein effektives Training.

**Erstellung einer classes.txt**
Die Datei "classes.txt" enthält die Klassennamen und die entsprechenden Klassenindizes in den Verzeichnissen "labels/train" und "labels/val".

**YAML-Datei**
Die YAML-Datei ist eine Konfigurationsdatei für das Training des YOLO-Modells und ist wie folgt strukturiert:
- `train`: Pfad zum Verzeichnis mit den Trainingsbildern.
- `val`: Pfad zum Verzeichnis mit den Validierungsbildern.
- `nc`: Anzahl der Klassen im Datensatz.
- `names`: Eine Liste der Klassennamen.
- `patience`: Anzahl der Epochen, die gewartet werden, wenn die Leistung des Modells sich nicht verbessert, bevor das Training beendet wird. Dies kann das Training automatisch bei Overfitting stoppen.
- `delta`: Schwellenwert, um zu bestimmen, ob die Leistung des Modells sich verbessert hat. Wenn die Verbesserung kleiner als dieser Schwellenwert ist, wird das Training gestoppt.

## YOLOv5 Training
Das YOLOv5-Repository wurde geklont und die Torch-Version überprüft. Wandb wurde für die Überwachung des Trainings verwendet. Dabei wurde die Datenkonfiguration aus data.yaml, das Modell aus yolov5s.yaml und die vorab trainierten Gewichte aus yolov5s.pt verwendet. Die Batch-Größe wurde auf 5 festgelegt, und während des Trainings wurden Metriken erfasst und in Wandb verfolgt.

## YOLOv5 Modell Test
... incoming

## Jump and Run Game
... incoming
