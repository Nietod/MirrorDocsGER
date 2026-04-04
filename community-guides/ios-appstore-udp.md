# iOS AppStore

**iOS AppStore UDP**

Mirrors standardmäßig eingesetzter KCP-Transport nutzt UDP-Sockets.\
Wenn du deine App zum ersten Mal zur Überprüfung im App Store einreichst, werden einige Apps abgelehnt, weil der VPN von Apple offenbar nicht mit UDP umgehen kann.

Wir wissen, warum das so ist, aber hier sind ein paar Workarounds, die einige vorschlagen:

* cooper: "Reiche deine App mit einem TCP-Transport wie Telepathy ein. Nach erfolgreicher Überprüfung wechsel beim nächsten Update wieder zu KCP. Das sollte funktionieren."
* Ninja: "Die Überprüfung der App ist immer wieder fehlgeschlagen, bis ich schließlich um eine manuelle Überprüfung gebeten habe, danach wurde sie genehmigt."
* Nutze den Multiplex-Transport für Veröffentlichungen im App Store, zum Beispiel KCP als primären Transport und Telepathy als Backup-Transport.

**iOS AppStore LAN-Übertragung**

Folge den Anweisungen von Xcode, um die Multicast-Netzwerkberechtigung von Apple zu erhalten.

Füge es zunächst dem App-Provisioning hinzu und aktiviere anschließend die entsprechende Capability in der App selbst. Stelle dabei sicher, dass das erforderliche Entitlement in Xcode korrekt hinterlegt ist.

Die neuesten Versionen brauchen möglicherweise Folgendes:  Füge NSLocalNetworkUsageDescription zu der info.plist hinzu.

\
Hinweise: Wenn LAN-Übertragung nicht funktioniert, versuche eine andere Adresse, ändere zum Beispiel 0.0.0.0 zu 255.255.255.255 (Denke daran nach jeder Änderung die App neu zu bauen)

Damit sollten die Netzwerk-Erkennungsfunktionen funktionieren. Ein großes Lob an overmatch-iman, Sylvain und andere Discord-Nutzer, die die funktionierenden Schritte geteilt haben.

