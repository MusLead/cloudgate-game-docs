# Eigenleistungen – Projekt Cloudgate

## Team 1: Leveleditor – Jatin, Pascal
- Entwicklung der gesamten Homepage-Navigation inkl. Level Selector,
  Charakterauswahl und Start-Menü (QML + C++ Backend)
- Implementierung des Leveleditors mit Tile Palette (links) und
  Level Canvas (rechts) als getrennte, koordinierte Komponenten
- Tile-Platzierung via Maus-Interaktion auf einem 20×25 Grid (32×32 px Tiles)
- Toolbar mit Back, Clear Level, Load/Save Level und +/-5 Row-Buttons
- Win Condition UI mit drei Modi (None, Timer bis 999s, Coins bis 99)
- Unterstützung von Normal Tiles (Index 0–126), Extra Tiles (1×2, Index 127+)
  sowie Background Button zur Hintergrundauswahl

---

## Team 2: Speichern & Laden – Agha, Homan
- Vollständige Implementierung des Persistenz-Layers für XML und HDF5
- Speichern von Level-Daten als XML inkl. Metadaten (Autor, Datum)
  und Validierung vor dem Speichern
- Tileset-Speicherung im HDF5-Format mit robuster Fehlerbehandlung
- XML-Parsing und HDF5-Dateizugriff beim Laden mit vollständiger
  Level-Rekonstruktion
- Kompatibilitätsprüfung beim Laden älterer oder fremder Level-Dateien
- Nahtlose Integration mit dem Leveleditor-Controller

---

## Team 3: Gameplay – Merlin
- Münz-System: Collectibles im Level verteilt mit Win-Condition-Unterstützung
- Health-System mit Herzen, Schaden-Management und Respawn-Logik
- Anzeige der Spielzeit im HUD mithilfe der NumberDigit-Klasse
  (erbt von AnimatedRenderable)
- Pausieren und Fortsetzen des Spiels (Pause/Resume-Funktionalität)
- Code Style Cleanup im gesamten Projekt
- Allgemeine Bugfixes und Verbesserungen der Spielstabilität

---

## Team 4: Physik – Celal Kir, Batuhan Akkaya
- Box2D Integration als System-Paket (libbox2d-dev) via CMake
  (Wechsel von FetchContent zu find_package)
- Physik-Architektur mit b2World, b2Body (Player) und ContactListener
- Update-Loop: onGround-Check per Raycast, Player Input zu Kräften & Impulsen,
  world->Step() mit 8/3 Iterationen
- Koordinaten-Konvertierung zwischen Box2D (32px = 1m, Y invertiert)
  und SDL (Top-Left-Koordinaten)
- Monster System mit Ghost & Snake: Patrouillen-Logik, Grid-Scan
  nach Tile-Paaren und Spawn als dynamischer Body
- Kollisions-Verhalten inkl. Power-Up-System, Update-Cycle,
  Bounding-Box Check, Schaden + Knockback und Invincibility-Cooldown