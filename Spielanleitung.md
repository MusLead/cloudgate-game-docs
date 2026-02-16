[[_TOC_]]

# Menü

Nach dem Start zeigt `Main.qml` drei Hauptpunkte:

- `Start`: Levelauswahl und Spielstart
- `LevelEditor`: Editor zum Erstellen/Bearbeiten von Levels
- `Characters`: Spielfigur auswählen

![title_screen](uploads/3fb2d5fe9f9f1cd2823e6dcff83bfd7a/title_screen.png){width=235 height=295}

# Level starten

Klickt man im Hauptmenü auf den Punkt `Start`, so gelangt man zur Levelauswahl:

![level_selection](uploads/0a0c669b2de81d118242eae1338fc988/level_selection.png){width=235 height=295}

Dort werden alle Level angezeigt, welche unter dem Ordner `res/*.xml` zu finden sind (außer `level_master.xml`).
Klickt man nun den Namen eines Levels an, so wird das Spiel in `LevelStarter.qml` im `GameView` gestartet.


## Steuerung im Spiel

- `Pfeil links/rechts`: Laufen
- `Leertaste`: Springen
- `A`: Figur nach links ausrichten
- `D`: Figur nach rechts ausrichten
- `P`: Pause
- `ESC`: Zurück zur vorherigen Seite

## Gegner

Im Spiel kann man Gegnern begegnen.

Die zu findenden Arten sind der Geist und die Schlange (die mehr wie eine Gurke aussieht).

Die Schlange bewegt sich von links nach rechts über den Boden, auf dem sie steht.

![enemy_snake](uploads/c39253c006d10f2d4567646e3f522316/enemy_snake.png){width=156 height=102}

Der Geist schwebt von links nach rechts durch die Luft.

![enemy_ghost](uploads/50f4897856405c6c5269f7fbebefa065/enemy_ghost.png){width=369 height=288}

Sobald er jedoch den Spieler bemerkt, fängt er an, ihn zu verfolgen.

![enemy_ghost_chase](uploads/881886338b08cdc77e928dc85a44f0ed/enemy_ghost_chase.png){width=287 height=268}

Glücklicherweise lässt er jedoch nach einiger Zeit auch wieder ab.

Berührt man einen Gegner, so erleidet der Spieler Rückstoß und verliert einen Lebenspunkt, repräsentiert durch dir Herzen in der oberen rechten Ecke des Bildschirms.

![enemies_and_taking_damage](uploads/ee2dd77bcd6a5077ffce15334fdf4384/enemies_and_taking_damage.png){width=235 height=295}

## Ein Level abschließen

Um ein Level erfolgreich abzuschließen, ist es immer nötig, ein offenes Tor am Ende zu erreichen.

![door](uploads/0f6fcc0d8bd9d42c4cf97e8015e1aa7a/door.png){width=200 height=159}

In den Leveldateien ist eine von drei Zieltypen definiert.
Je nach Konfiguration können weitere Bedingungen nötig sein, um ein Level erfolgreich abzuschließen:

- `0` (`GOAL_NONE`): Kein spezielles Ziel.
- `1` (`GOAL_COINS`): Genug Coins sammeln, um das Tor zu öffnen.
- `2` (`GOAL_TIME`): Ausgang vor Ablauf des Timers erreichen.

Sollte die Zielbedingung nicht erfüllt sein, bleibt das Tor geschlossen:

![door_closed](uploads/8b85eb3c29131a6bcc1049b9958e59aa/door_closed.png){width=200 height=159}

Die für den Zieltyp "Coins" benötigten Münzen kann man unterhalb der Lebenspunkte des Spielers sehen (auch in Leveln mit anderen Zieltypen).

![coins](uploads/924c2bf4565c0bed82260c88fd24d51e/coins.png){width=235 height=295}

## Game Over / Level Ende

Ein Game Over passiert durch folgende Bedingungen:

- Keine Lebenspunkte mehr übrig (HP <= 0)
- Zeitlimit überschritten (bei Zeit-Ziel)
- Spieler fällt in den kritischen unteren Kamerabereich

![death_zone](uploads/825d56846a9b56fba74895c5e4b55f9d/death_zone.png){width=235 height=295}

# Level Editor
Wählt man im Startmenü die Option `LevelEditor` aus, so gelangt man zum [Level-Editor](Level-Editor), welcher auf seiner eigenen Seite dokumentiert ist.

# Charakterauswahl

Wählt man im Menü `Characters` aus, so kommt man zur Charakterauswahl.

- Pfeile links/rechts wechseln die Figur.
- Beim Zurückgehen (`Back`) wird der Character in allen `res/*.xml` Leveldateien aktualisiert.