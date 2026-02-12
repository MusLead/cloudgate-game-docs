## Hinzufügen neuer Level

1. Erstelle eine neue `level.xml`-Datei im `res/`-Verzeichnis
2. Erstelle die entsprechende `level.h5`-Datei mit den Level-Daten
3. Ändere den `levelPath` in `SecondPage.qml` oder setze ihn programmatisch

## Anpassen der Spiel-Physik

Die Physik-Parameter können in der `level.xml` angepasst werden:
- `gravity_x`, `gravity_y`: Gravitationskräfte
- `damping_x`, `damping_y`: Dämpfung
- `jump_force_y`: Sprungkraft
- `max_run_velocity`: Maximale Laufgeschwindigkeit
- `max_fall_velocity`: Maximale Fallgeschwindigkeit
- `max_jump_height`: Maximale Sprunghöhe

## Anpassen der Spiel-Größe

Die Spiel-Größe ist fest auf 800x600 Pixel eingestellt. Um sie zu ändern:

1. Ändere `m_gameWidth` und `m_gameHeight` in `GameView.cpp`
2. Passe die Größe in `SecondPage.qml` an

## Anpassen der Kamera-Position

Die Kamera-Position kann in `src/game/Level.cpp` angepasst werden:

```cpp
Level::Level(MainWindow* mainWindow, std::string filename)
    : StaticRenderable(mainWindow),
      m_mainWindow(mainWindow),
      m_camera(400, 600, mainWindow->w(), mainWindow->h()),  // X, Y, Breite, Höhe
      m_layers(&m_camera)
```

- **X-Position**: Horizontale Startposition der Kamera (Standard: 400)
- **Y-Position**: Vertikale Startposition der Kamera (Standard: 600)
- Die Kamera scrollt nur vertikal (feste X-Position), folgt dem Spieler aber in Y-Richtung

### Anpassen der Y-Position (Kamera, Spieler, Karte)

Um alles weiter unten zu positionieren, können folgende Positionen angepasst werden:

1. **Kamera Y-Position**: In `src/game/Level.cpp` Zeile 34, zweiter Parameter
2. **Spieler Y-Position**: In `res/level.xml`, `<position_y>` Tag
3. **Karte Y-Offset**: In `src/game/TileSet.cpp` Zeile 164, `target.y` Berechnung (+600 Offset)

**Beispiel:**
- Kamera: `m_camera(400, 600, ...)` → Y=600
- Spieler: `<position_y>600</position_y>` → Y=600
- Karte: `target.y = ... + 600` → Y-Offset von 600

Die Kollisionserkennung in `Physics.cpp` wurde entsprechend angepasst, um den Y-Offset zu berücksichtigen.

### Performance-Optimierungen

Das Rendering kopiert bei jedem Frame die Pixel vom SDL2-Renderer. Mögliche Optimierungen:

1. **Textur-basiertes Rendering**: Verwende `SDL_Texture` statt `SDL_Surface`
2. **Framerate-Limitierung**: Reduziere die Update-Rate bei niedriger Priorität
3. **Pufferung**: Puffere das gerenderte Bild und aktualisiere nur bei Änderungen
