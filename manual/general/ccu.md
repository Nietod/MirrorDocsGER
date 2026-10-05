---
description: 'Eine der am häufigsten gestellten Fragen: Wie viele CCU schafft Mirror?'
---

# CCU

Eine ähnliche Frage kam vor einiger Zeit in den [Unity-Foren](https://forum.unity.com/threads/stress-test-using-unity-as-server.1126640/#post-7245842) auf, deshalb kopiere ich meine Antwort hierher, falls sie noch jemandem nützt.

![Unser ruckelnder Test mit 480 CCU aus dem Jahr 2019](../../.gitbook/assets/2021-06-17\_12-24-46@2x.png)

Eines der [mit Mirror entwickelten](https://github.com/vis2k/Mirror#made-with-mirror) MMOs hatte zum Start ziemlich viele CCU, ich glaube, es war Inferna.\
Sie haben die Karte in getrennte Serverinstanzen aufgeteilt, mit einem Limit von etwa 200 CCU pro Karte.\
Ich müsste es noch einmal nachschlagen, aber ich glaube, auf diese Weise wurden zeitweise rund 1000 CCU pro Welt erreicht.\
\
Es gibt außerdem ein [sehr altes Video](https://www.youtube.com/watch?v=mDCNff1S9ZU\&t=58s), in dem wir den schlimmsten Fall mit 480 CCU ausprobieren, alle an einem Ort wie in deinem Video. Es ruckelt höllisch, aber der Server hat problemlos durchgehalten.\
\
Sowohl Inferna als auch das Video mit 480 CCU nutzen alte Versionen von Mirror und Unity. Seitdem gab es jahrelang Verbesserungen bei Mirror, Unity und der Serverhardware.\
\
Aus Mirror lassen sich noch jede Menge Optimierungen herausholen. Danach ist etwa gegen Ende dieses Jahres ein weiterer CCU-Test geplant.\
\
Bedenke, dass auch die Komplexität deines Spiels eine große Rolle spielt. Ein 3D-MMO mit physikbasierter Bewegung wie WoW lässt sich deutlich schwerer skalieren als ein 2D-MMO mit Click-to-Move-Steuerung. Für Indie-Entwickler ist 2D wirklich eine Überlegung wert. Es ist deutlich günstiger, viel einfacher umzusetzen und skaliert dank weniger komplexer Physik, Meshes usw. wesentlich besser.\
\
Letztendlich gibt es in der MonoBehaviour-Welt definitiv eine Grenze für das, was wir erreichen können.\
Für 1500 Spieler mit physikbasierter Bewegung wie in WoW bräuchtest du auf jeden Fall DOTS oder einen Server, der nicht in Unity läuft.\
\
Meiner Meinung nach sind Unity und MonoBehaviour trotzdem eine gute Wahl. Es ist besser, ein MMO mit nur 500 CCU und 250 CCU pro Instanz zu **veröffentlichen**, als ein MMO mit 1500 CCU **nie zu veröffentlichen**.
