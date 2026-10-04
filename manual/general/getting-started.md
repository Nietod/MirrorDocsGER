# Erste Schritte

Dieses Dokument beschreibt Schritte, wie du mit Mirror ein Mehrspielerspiel erstellst. Der Ablauf ist eine vereinfachte und übergeordnete Fassung dessen, was bei einem echten Spiel nötig ist. In der Praxis läuft nicht immer alles genau so ab, aber du bekommst damit eine Grundlage für dein eigenes Vorgehen.

## Videotutorials <a href="#video-tutorials" id="video-tutorials"></a>

Sieh dir diese [großartigen Videos](../../community-guides/video-tutorials.md) an, die dir den Einstieg in Mirror zeigen.

## Skriptvorlagen <a href="#script-templates" id="script-templates"></a>

* Erstelle neue NetworkBehaviours und andere gängige Skripte schneller

Siehe [Skriptvorlagen](script-templates.md).

## Network Manager einrichten <a href="#networkmanager-set-up" id="networkmanager-set-up"></a>

* Erstelle einen neuen Network Manager über das Menü [Assets > Create > Mirror](script-templates.md).
* Füge der Szene ein neues GameObject hinzu und benenne es in „NetworkManager“ um.
* Füge dem GameObject „NetworkManager“ die neu erstellte Network-Manager-Komponente hinzu.
* Füge dem GameObject die Komponente [NetworkManagerHUD](../components/network-manager-hud.md) hinzu. Sie stellt die Standardoberfläche bereit, mit der du den Zustand des Netzwerkspiels verwaltest.

Siehe [Den NetworkManager verwenden](../components/network-manager.md).

## Spieler-Prefab <a href="#player-prefab" id="player-prefab"></a>

* Suche das Prefab für das Spieler-GameObject in deinem Spiel oder erstelle ein Prefab aus dem Spieler-GameObject
* Füge dem Spieler-Prefab die Komponente NetworkIdentity hinzu
* Weise im Abschnitt „Spawn Info“ des NetworkManager dem Feld `Player Prefab` das Spieler-Prefab zu
* Entferne die Instanz des Spieler-GameObjects aus der Szene, falls sie dort vorhanden ist

Mehr dazu findest du unter [Spieler-GameObjects](../guides/gameobjects/player-gameobjects.md).

## Spielerbewegung <a href="#player-movement" id="player-movement"></a>

* Füge dem Spieler-Prefab die Komponente NetworkTransform hinzu
* Aktiviere an der Komponente die Checkbox „Client Authority“.
* Passe Eingabe- und Steuerungsskripte so an, dass sie `isLocalPlayer` berücksichtigen
* Überschreibe OnStartLocalPlayer, um für den Spieler die Kontrolle über die Main Camera der Szene zu übernehmen.

Dieses Skript verarbeitet zum Beispiel nur die Eingaben des lokalen Spielers:

```csharp
using UnityEngine;
using Mirror;

public class Controls : NetworkBehaviour
{
    void Update()
    {
        // exit from update if this is not the local player
        if (!isLocalPlayer) return;

        // handle player input for movement
    }
}
```

## Grundlegender Spielzustand des Spielers <a href="#basic-player-game-state" id="basic-player-game-state"></a>

* Mache Skripte, die wichtige Daten enthalten, zu NetworkBehaviours statt MonoBehaviours
* Mache wichtige Klassenvariablen zu SyncVars

Siehe [Zustandssynchronisation](../guides/synchronization/).

## Remote Actions <a href="#networked-actions" id="networked-actions"></a>

* Mache Skripte, die wichtige Aktionen ausführen, zu NetworkBehaviours statt MonoBehaviours
* Wandle Funktionen, die wichtige Spieleraktionen ausführen, in Commands um

Siehe [Remote Actions](../guides/communications/remote-actions.md).

## GameObjects, die keine Spieler sind <a href="#non-player-game-objects" id="non-player-game-objects"></a>

Passe Prefabs an, die keine Spieler sind, zum Beispiel Gegner:

* Füge die Komponente NetworkIdentity hinzu
* Füge die Komponente NetworkTransform hinzu
* Registriere spawnbare Prefabs beim NetworkManager
* Passe Skripte mit Spielzustand und Aktionen an

## Spawner <a href="#spawners" id="spawners"></a>

* Mache Spawner-Skripte gegebenenfalls zu NetworkBehaviours
* Ändere Spawner so, dass sie nur auf dem Server laufen (nutze die Eigenschaft isServer oder die Funktion `OnStartServer()`)
* Rufe für erstellte GameObjects `NetworkServer.Spawn()` auf

## Spawnpositionen für Spieler <a href="#spawn-positions-for-players" id="spawn-positions-for-players"></a>

* Füge ein neues GameObject hinzu und platziere es an der Startposition des Spielers
* Füge dem neuen GameObject die Komponente NetworkStartPosition hinzu
