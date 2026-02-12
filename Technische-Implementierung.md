### SDL2-Integration in Qt/QML

Das Projekt verwendet einen innovativen Ansatz, um SDL2 direkt in Qt/QML einzubetten:

#### 1. Verstecktes SDL2-Fenster

Die `MainWindow`-Klasse wurde modifiziert, um ein verstecktes SDL2-Fenster zu erstellen:

```cpp
// In src/game/MainWindow.cpp
m_window = SDL_CreateWindow(
    "Jumper Main Window",
    SDL_WINDOWPOS_UNDEFINED,
    SDL_WINDOWPOS_UNDEFINED,
    m_width,
    m_height,
    SDL_WINDOW_HIDDEN  // Verstecktes Fenster!
);
```

#### 2. GameView - QML-Integration

Die `GameView`-Klasse (`GameView.hpp`/`GameView.cpp`) ist ein `QQuickPaintedItem`, das:

- SDL2 mit verstecktem Fenster initialisiert
- Den SDL2-Renderer-Inhalt in eine `QImage` kopiert
- Diese `QImage` in QML rendert
- Tastatur-Events von Qt zu SDL konvertiert

**Wichtigste Methoden:**

```cpp
class GameView : public QQuickPaintedItem
{
    // Rendert SDL2-Inhalt in QML
    void paint(QPainter *painter) override;
    
    // Startet das Spiel
    void startGame();
    
    // Stoppt das Spiel
    void stopGame();
    
    // Update-Loop (60 FPS)
    void updateGame();
    
    // Konvertiert Qt-Tastatur-Events zu SDL
    void keyPressEvent(QKeyEvent *event) override;
    SDL_Keycode convertQtKeyToSDL(int qtKey);
};
```

#### 3. Rendering-Pipeline

Das Rendering funktioniert folgendermaßen:

1. **SDL2-Rendering**: Das Spiel rendert in den SDL2-Renderer (verstecktes Fenster)
2. **Pixel-Kopie**: `SDL_RenderReadPixels()` kopiert die Pixel in eine `SDL_Surface`
3. **QImage-Konvertierung**: Die `SDL_Surface` wird zu einer `QImage` konvertiert
4. **QML-Darstellung**: Die `QImage` wird im `paint()`-Handler von `QQuickPaintedItem` gezeichnet

**Code-Ausschnitt aus GameView.cpp:**

```cpp
void GameView::paint(QPainter *painter)
{
    // Render game to SDL renderer
    m_gameWindow->render();
    
    // Copy SDL renderer content to QImage
    SDL_Surface* surface = SDL_CreateRGBSurface(0, m_gameWidth, m_gameHeight, 32,
                                                  0x00FF0000, 0x0000FF00, 0x000000FF, 0xFF000000);
    
    // Read pixels from renderer
    SDL_RenderReadPixels(renderer, NULL, SDL_PIXELFORMAT_ARGB8888, 
                        surface->pixels, surface->pitch);
    
    // Convert SDL surface to QImage
    QImage image(static_cast<uchar*>(surface->pixels), 
                 surface->w, surface->h, surface->pitch, 
                 QImage::Format_ARGB32);
    
    // Draw image to painter
    painter->drawImage(boundingRect(), image.copy());
    SDL_FreeSurface(surface);
}
```

#### 4. Tastatur-Event-Weiterleitung

Qt-Tastatur-Events werden zu SDL-Events konvertiert:

```cpp
void GameView::keyPressEvent(QKeyEvent *event)
{
    SDL_Event sdlEvent;
    sdlEvent.type = SDL_KEYDOWN;
    sdlEvent.key.keysym.sym = convertQtKeyToSDL(event->key());
    SDL_PushEvent(&sdlEvent);
}

SDL_Keycode GameView::convertQtKeyToSDL(int qtKey)
{
    switch (qtKey) {
        case Qt::Key_Left: return SDLK_LEFT;
        case Qt::Key_Right: return SDLK_RIGHT;
        case Qt::Key_Space: return SDLK_SPACE;
        case Qt::Key_A: return SDLK_a;
        case Qt::Key_D: return SDLK_d;
        default: return SDLK_UNKNOWN;
    }
}
```

#### 5. MainWindow-Erweiterungen

Die `MainWindow`-Klasse wurde um folgende Methoden erweitert:

```cpp
class MainWindow {
    // Manuelles Update (ohne run()-Loop)
    void update(const Uint8* keystates);
    
    // Manuelles Rendering
    void render();
    
    // Zugriff auf Level
    Level* level();
};
```

Diese Methoden ermöglichen es, das Spiel außerhalb der `run()`-Methode zu steuern.

### Update-Loop

Der Update-Loop läuft über einen `QTimer` mit 60 FPS (16ms Intervall):

```cpp
m_updateTimer = new QTimer(this);
connect(m_updateTimer, &QTimer::timeout, this, &GameView::updateGame);
m_updateTimer->start(16); // 60 FPS
```

In `updateGame()`:
1. SDL-Events werden verarbeitet
2. Tastatur-Zustand wird abgerufen
3. `MainWindow::update()` wird aufgerufen
4. `update()` wird aufgerufen, um `paint()` zu triggern