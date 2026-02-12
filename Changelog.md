## Version 0.3
- **ESC-Taste**: Führt jetzt direkt zurück zum Hauptmenü (statt Pause-Menü)
- **Kamera-Verhalten**: Kamera hat jetzt eine feste X-Position und scrollt nur vertikal (oben/unten)
- **Kamera-Position**: Kann in `Level.cpp` angepasst werden (Standard: X=400, Y=600)
- **Level-Grenzen**: Linke und rechte Ränder des Levels fungieren jetzt als Kollisionsflächen
- **Y-Position Anpassungen**: Kamera, Spieler und Karte können weiter unten positioniert werden
- **Sicherheits-Fixes**: Grenzprüfungen für negative Tile-Koordinaten hinzugefügt, um Speicherzugriffsfehler zu vermeiden
  - `TileArray::get()` prüft jetzt auf negative Werte
  - `TileTree::get()` prüft jetzt auf negative Indizes
  - `Physics::resolveCollision()` prüft jetzt auf negative Tile-Koordinaten
  - `Physics::resolveCollision()` prüft jetzt Level-Grenzen (links/rechts) und stoppt den Spieler

## Version 0.2
- **SDL2-Einbettung**: Spiel läuft jetzt direkt im Qt-Fenster, nicht mehr in separatem Fenster
- **GameView**: Neue Klasse zum Einbetten von SDL2 in QML
- **Rendering-Pipeline**: SDL2 → QImage → QML
- **Tastatur-Event-Weiterleitung**: Automatische Konvertierung von Qt- zu SDL-Events
- **MainWindow-Erweiterungen**: Neue Methoden für manuelles Update/Rendering

## Version 0.1
- Initiale Integration der Spiel-Engine aus uebung10
- Qt/QML-Benutzeroberfläche
- GameController für Spiel-Verwaltung (separates Fenster)
- Level-Laden aus HDF5-Dateien
