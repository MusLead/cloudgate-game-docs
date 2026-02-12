### Von uebung10 integriert

1. **Physik-System** (`src/game/Physics.*`)
   - Kollisionserkennung mit Tiles
   - Gravitation und Dämpfung
   - Sprung-Mechanik mit maximaler Sprunghöhe
   - Geschwindigkeitsbegrenzungen

2. **Level-System** (`src/game/Level.*`)
   - Laden von Leveln aus XML/HDF5-Dateien
   - Unterstützung für Hintergrund- und Kollisions-Tiles
   - Layer-Management für Rendering-Reihenfolge

3. **Camera-System** (`src/game/Camera.*`)
   - Automatisches Folgen der Spielfigur (nur vertikal)
   - Feste X-Position: Die Kamera scrollt nur nach oben/unten, nicht horizontal
   - Welt-zu-Bildschirm-Koordinaten-Transformation
   - Kamera-Position kann in `Level.cpp` angepasst werden

4. **Actor-System** (`src/game/Actor.*`)
   - Animierte Spielfigur
   - Physikalische Eigenschaften (Kräfte, Geschwindigkeiten)
   - Sprung- und Bewegungslogik

5. **Tile-System** (`src/game/TileSet.*`)
   - Rendering von Tile-Maps
   - Kollisionserkennung basierend auf Tile-Indizes
   - Unterstützung für verschiedene Tile-Sets

### Qt/QML Integration

- **GameView**: `QQuickPaintedItem`, das SDL2 direkt in QML einbettet
- **SecondPage.qml**: QML-Seite mit eingebettetem Spiel
- **Tastatur-Event-Handling**: Automatische Konvertierung von Qt- zu SDL-Events
- **Rendering-Pipeline**: SDL2 → QImage → QML

### GameView in QML

```qml
import Cloudgate_game 1.0

GameView {
    id: gameView
    width: 800
    height: 600
    
    onGameStarted: {
        console.log("Game started")
    }
    
    onGameStopped: {
        console.log("Game stopped")
    }
    
    // Spiel starten
    Component.onCompleted: {
        gameView.startGame()
    }
}
```

### Properties

- `levelPath` (QString): Pfad zur Level-XML-Datei
- `running` (bool): Ob das Spiel läuft (read-only)

### Signals

- `gameStarted()`: Wird emittiert, wenn das Spiel startet
- `gameStopped()`: Wird emittiert, wenn das Spiel stoppt
- `levelPathChanged()`: Wird emittiert, wenn der Level-Pfad geändert wird
- `runningChanged()`: Wird emittiert, wenn der Running-Status sich ändert

### Slots

- `startGame()`: Startet das Spiel
- `stopGame()`: Stoppt das Spiel