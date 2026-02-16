# Spielanleitung

## Menü

Nach dem Start zeigt `Main.qml` drei Hauptpunkte:

- `Start`: Levelauswahl und Spielstart
- `LevelEditor`: Editor zum Erstellen/Bearbeiten von Levels
- `Characters`: Spielfigur auswählen

![title_screen](uploads/3fb2d5fe9f9f1cd2823e6dcff83bfd7a/title_screen.png){width=479 height=596}

## Level starten

Klickt man im Hauptmenü auf den Punkt `Start`, so gelangt man zur Levelauswahl:

![level_selection](uploads/0a0c669b2de81d118242eae1338fc988/level_selection.png){width=479 height=599}

Dort werden alle Level angezeigt, welche unter dem Ordner `res/*.xml` zu finden sind (außer `level_master.xml`).
Klickt man nun den Namen eines Levels an, so wird das Spiel in `LevelStarter.qml` im `GameView` gestartet.


### Steuerung im Spiel

- `Pfeil links/rechts`: Laufen
- `Leertaste`: Springen
- `A`: Figur nach links ausrichten
- `D`: Figur nach rechts ausrichten
- `P`: Pause
- `ESC`: Zurück zur vorherigen Seite

### Gegner

Im Spiel kann man Gegnern begegnen, wie bereits in Level Editor beschrieben.
Berührt man einen Gegner, so erleidet der Spieler Rükstoß und verliert einen Lebenspunkt, repräsentiert durch dir Herzen in der oberen rechten Ecke des Bildschirms.

![enemies_and_taking_damage](uploads/ee2dd77bcd6a5077ffce15334fdf4384/enemies_and_taking_damage.png){width=475 height=600}

### Ein Level abschließen

Um ein Level erfolgreich abzuschließen, ist es immer nötig, ein offenes Tor am Ende zu erreichen.

![door](uploads/0f6fcc0d8bd9d42c4cf97e8015e1aa7a/door.png){width=200 height=159}

In den Leveldateien ist eine von drei Zieltypen definiert.
Je nach Konfiguration können weitere Bedingungen nötig sein, um ein Level erfolgreich abzuschließen:

- `0` (`GOAL_NONE`): Kein spezielles Ziel.
- `1` (`GOAL_COINS`): Genug Coins sammeln, um das Tor zu öffnen.
- `2` (`GOAL_TIME`): Ausgang vor Ablauf des Timers erreichen.

Sollte die Zielbedingung nicht erfüllt sein, bleibt das Tor geschlossen:

![door_closed](uploads/8b85eb3c29131a6bcc1049b9958e59aa/door_closed.png){width=127 height=100}

Die für den Zieltyp "Coins" benötigten Münzen kann man unterhalb der Lebenspunkte des Spielers sehen (auch in Leveln mit anderen Zieltypen).

![coins](uploads/924c2bf4565c0bed82260c88fd24d51e/coins.png){width=478 height=600}

### Game Over / Level Ende

Ein Game Over passiert durch folgende Bedingungen:

- Keine Lebenspunkte mehr übrig (HP <= 0)
- Zeitlimit überschritten (bei Zeit-Ziel)
- Spieler fällt in den kritischen unteren Kamerabereich

![death_zone](uploads/825d56846a9b56fba74895c5e4b55f9d/death_zone.png){width=475 height=600}

## Charakterauswahl

Wählt man im Menü `Characters` aus, so kommt man zur Charakterauswahl.

- Pfeile links/rechts wechseln die Figur.
- Beim Zurückgehen (`Back`) wird der Character in allen `res/*.xml` Leveldateien aktualisiert.