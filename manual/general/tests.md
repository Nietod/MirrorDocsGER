---
description: Mirrors Geheimrezept.
---

# Unit Tests

Viele Entwickler sind überrascht, wie stabil Mirror im Vergleich zu dem ist, was sie vorher verwendet haben.

Das ist kein Zufall. Mirror wird **intensiv** getestet mit:

* \> **1400** Unit Tests
* \~ **80 %** Testabdeckung

![\[2021-06-17\] Mirror-Testabdeckung von 79,6 % einschließlich aller \[Obsoletes\]](<../../.gitbook/assets/2021-06-17 - 79,6 percent - including obsoletes.png>)

{% hint style="success" %}
Soweit wir wissen, hat **Mirror** die höchste Testabdeckung aller `MonoBehaviour`-Netzwerkbibliotheken für **Unity**.
{% endhint %}

Anders gesagt sind 80 % unseres Codes **durch Tests abgedeckt**, die sicherstellen, dass er für eine gegebene Eingabe immer die korrekte Ausgabe liefert. In der Praxis bedeutet das:

*   Wenn du **einen Bug meldest**, beheben wir ihn in der Regel und fügen einen Test hinzu, der garantiert, dass er **nie** wieder auftritt.

    Falls wir **versehentlich** einen Bug einbauen, fangen ihn unsere Tests höchstwahrscheinlich sofort ab, bevor du ihm in deinem Spiel überhaupt begegnest.
* Wir können bestehende Funktionen bedenkenlos **verbessern**. Wenn eine Neufassung nicht exakt dieselbe Ausgabe liefert wie die vorherige Version, fangen unsere Tests das ab.

{% hint style="success" %}
Als **Faustregel** gilt: Wenn du während der Entwicklung auf einen Mirror-Bug stößt, haben wir diesen Teil des Codes schlicht noch nicht mit Tests abgedeckt.
{% endhint %}

![](../../.gitbook/assets/2021-05-20\_16-06-57@2x.png)

Wenn du Mirror aus dem **Asset Store** herunterlädst, siehst du diese Tests nicht, weil wir dich nicht damit belasten wollen. Es gibt sie nur auf **GitHub**.

## Code-Coverage-Einstellungen

Um die Coverage-Ergebnisse zu reproduzieren, verwende Unitys Code-Coverage-Paket und führe alle unsere Edit-Mode-Tests aus.

![Code-Coverage-Einstellungen](../../.gitbook/assets/\_SETTINGS\_.png)

## MirrorTest

Wenn du Tests beisteuern oder bestehende aufräumen möchtest, bitte nur zu!

Sieh dir die Basisklassen `MirrorEditModeTest` und `MirrorPlayModeTest` an. Sie stellen einige Hilfsfunktionen und ein Setup bereit, die wir für die meisten unserer Tests verwenden, zum Beispiel das Erstellen eines Netzwerkobjekts mit einigen Netzwerkkomponenten.
