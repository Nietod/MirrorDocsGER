# Allgemein

Mirror ist ein System, mit dem du Unity-Spiele um Mehrspielerfunktionen erweiterst. Es baut auf der tiefer liegenden Transportschicht für Echtzeitkommunikation auf und übernimmt viele der üblichen Aufgaben, die Mehrspielerspiele erfordern. Die Transportschicht unterstützt jede Art von Netzwerktopologie, jedoch ist Mirror selbst ein serverautoritäres System. Trotzdem kann einer der Teilnehmer gleichzeitig Client und Server sein, sodass kein dedizierter Serverprozess nötig ist. Zusammen mit den Internetdiensten lassen sich so Mehrspielerspiele mit wenig Aufwand für Entwickler über das Internet spielen.

Mirror legt den Fokus auf einfache Bedienung und iterative Entwicklung und bietet nützliche Funktionen für Mehrspielerspiele, zum Beispiel:

* Message Handlers
* Leistungsstarke Allzweck-Serialisierung
* Verteilte Objektverwaltung
* Zustandssynchronisation
* Netzwerkklassen: Server, Client, Connection usw.

Mirror besteht aus mehreren Schichten, die jeweils Funktionen hinzufügen:

![](<../../.gitbook/assets/image (111).png>)

## Server und Host <a href="#server-and-host" id="server-and-host"></a>

Mirror-Mehrspielerspiele beinhalten:

* **Server**\
  Ein Server ist eine Instanz des Spiels, mit der sich alle anderen Spieler verbinden, wenn sie zusammen spielen wollen. Ein Server verwaltet oft verschiedene Aspekte des Spiels, wie etwa den Punktestand und überträgt diese Daten zurück an die Clients.
* **Clients**\
  Clients sind Instanzen des Spiels, die sich in der Regel von anderen Computern aus mit dem Server verbinden. Clients können sich über ein lokales Netzwerk oder online verbinden.

Ein Client ist eine Instanz des Spiels, die sich mit dem Server verbindet, damit die Person, die es spielt, mit anderen Leuten spielen kann, die sich jeweils über ihre eigenen Clients verbinden.

Der Server kann entweder ein „dedizierter Server“ oder ein „Host-Server“ sein.

* **Dedizierter Server**\
  Eine Instanz des Spiels, die ausschließlich als Server läuft.
* **Host-Server**\
  Wenn es keinen dedizierten Server gibt, übernimmt einer der Clients zusätzlich die Rolle des Servers. Dieser Client ist der „Host-Server“. Der Host-Server erstellt eine einzige Instanz des Spiels (den Host), die gleichzeitig als Server und Client fungiert.

Das Diagramm unten zeigt drei Spieler in einem Mehrspielerspiel. In diesem Spiel fungiert ein Client zugleich als Host, das heißt, dieser Client ist der „lokale Client“. Der lokale Client verbindet sich mit dem Host-Server, wobei beide auf demselben Computer laufen. Die anderen beiden Spieler sind Remote-Clients. Sie sitzen also an anderen Computern und sind mit dem Host-Server verbunden.

![](<../../.gitbook/assets/image (86).png>)

Der Host ist eine einzige Instanz deines Spiels, die gleichzeitig als Server und Client fungiert. Für die Kommunikation mit dem lokalen Client nutzt der Host eine spezielle Art von internem Client, während alle anderen Clients Remote-Clients sind. Der lokale Client kommuniziert mit dem Server über direkte Funktionsaufrufe und Nachrichtenwarteschlangen, da er im selben Prozess läuft. Er teilt sich sogar die Szene mit dem Server. Remote-Clients kommunizieren mit dem Server über eine normale Netzwerkverbindung. Wenn du Mirror verwendest, wird all das automatisch für dich erledigt.

Ein Ziel des Mehrspielersystems ist, dass der Code für lokale Clients und Remote-Clients derselbe ist, sodass du bei der Entwicklung deines Spiels meistens nur an eine Art von Client denken musst. In den meisten Fällen behandelt Mirror diesen Unterschied automatisch, sodass du selten darüber nachdenken musst, ob dein Code auf einem lokalen Client oder einem Remote-Client läuft.

## Instanziieren und Spawnen <a href="#instantiate-and-spawn" id="instantiate-and-spawn"></a>

Wenn du in Unity ein Einzelspielerspiel entwickelst, verwendest du normalerweise die Methode `GameObject.Instantiate`, um zur Laufzeit neue GameObjects zu erstellen. In einem Mehrspielersystem muss jedoch der Server selbst GameObjects „spawnen“, damit sie im vernetzten Spiel aktiv sind. Wenn der Server GameObjects spawnt, werden diese auch auf den verbundenen Clients erzeugt. Das Spawnsystem verwaltet den Lebenszyklus des GameObjects und synchronisiert seinen Zustand, je nachdem, wie du das GameObject eingestellt hast.

Mehr zum vernetzten Instanziieren und Spawnen findest du in der Dokumentation zum Spawnen von [GameObjects](../guides/gameobjects/).

## Spieler und lokale Spieler <a href="#players-and-local-players" id="players-and-local-players"></a>

Mirror behandelt Spieler-GameObjects anders als GameObjects, die keine Spieler sind. Wenn ein neuer Spieler dem Spiel beitritt (also ein neuer Client sich mit dem Server verbindet), wird das GameObject dieses Spielers auf seinem Client zum „lokalen Spieler“-GameObject. Mirror verknüpft die Verbindung des Spielers mit seinem GameObject. Mirror ordnet jeder Person, die das Spiel spielt, ein Spieler-GameObject zu und leitet Netzwerk-Befehle an dieses einzelne GameObject weiter. Ein Spieler kann keinen Befehl auf dem GameObject eines anderen Spielers aufrufen, sondern nur auf seinem eigenen.

Mehr dazu findest du in der Dokumentation zu [Spieler-GameObjects](../guides/gameobjects/player-gameobjects.md).

## Autorität

Sowohl Server als auch Clients können das Verhalten eines GameObjects steuern. Der Begriff „Autorität“ beschreibt, wie und wo ein GameObject verwaltet wird. Mirror geht standardmäßig von „Serverautorität“ aus, bei der der Server die Autorität über alle GameObjects hat. Spieler-GameObjects sind ein Sonderfall und haben „lokale Autorität“. Es kann sein, dass du dein Spiel mit einem anderen Autoritätssystem bauen willst. Mehr dazu findest du unter [Netzwerkautorität](../guides/authority.md).
