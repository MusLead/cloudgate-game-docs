# Level-Editor

[[_TOC_]]

## Überblick

Der Editor ist in `qml/LevelEditor.qml` umgesetzt und wird von `LevelEditorController` gesteuert.

Aufbau:

- Links: `TilesetPalette` (Tile-Auswahl)
- Rechts: `LevelCanvas` (Level-Fläche)
- Oben: Toolbar (Save/Load/Clear/Background/Rows/Goal/ScrollSpeed)

![level_editor](uploads/8b1ba724408ba5c7ad608e5ef80fb740/level_editor.png){width=307 height=300}

## Grund-Workflow

1. `LevelEditor` im Hauptmenue starten.
2. Tile links auswaehlen.
3. Auf der rechten Canvas platzieren.
4. Mit `Save` speichern (XML + H5).

## Bedienung

- Linksklick auf Canvas: Tile setzen
- Rechtsklick auf Canvas: Tile loeschen
- Rahmen-Tiles (Rand) sind geschuetzt
- Spawnbereich des Spielers (2x2 Feld unten links) ist geschuetzt

## Tile-Sets

Es gibt zwei Modi:

- Normal (`1x1` Tiles)
- Extra (`1x2` Tiles), über Switch aktivierbar

Beim 1x2-Modus werden zusammengehoerende Tile-Paare gesetzt/entfernt.

## Grid-Grösse

- `+ 5 Tile above`: fügt oben 5 Reihen hinzu
- `- 5 Tile above`: entfernt oben Reihen (Minimum Höhe bleibt 25)

## Win-Condition und Scroll-Speed

In der Top-Leiste:

- Scroll-Speed (Slider, intern Faktor 4)
- Zieltyp:
  - None
  - Coins (mit Wert)
  - Time (mit Sekundenwert)

![level_editor_win_cons](uploads/029c2874b02e18ccf6f588c2171f40fd/level_editor_win_cons.png){width=158 height=63}

Falls beim Coin-Ziel der eingetragene Wert höher als die Anzahl der im Level vorhandenen Coins eingestellt sein sollte, so wird er beim Speichern automatisch auf die im Level vorhandenen Coins begrenzt.


## Hintergrund

`Background` erlaubt die Auswahl eines Bildes aus:

- `res/images/backgrounds/`

![level_editor_menu](uploads/5ad94523fced5e794dacd63eea8887a3/level_editor_menu.png){width=258 height=198}

Der Hintergrundpfad wird in XML als `background_path` gespeichert.
Wenn weitere Bilder dem Ordner hinzugefügt werden, müssen diese ebenfalls in `res/assets.qrc` hinzugefügt werden, um verwendet werden zu können.

## Save/Load

`Save` erzeugt die beiden folgenden Dateien:

- `levelname.xml`
- `levelname.h5`

Bei `Load` wird die xml eines gespeicherten Levels ausgewählt und in den Leveleditor geladen.
Dazu muss ebenso eine passende HDF5 (.h5) Datei im selben Ordner vorhanden sein.
Die geladenen Daten teilen sich wie folgt auf:

- XML-Metadaten: Goal, Tilegrößen, Hintergrund etc.
- HDF5-Daten: Tiles + Texturen.