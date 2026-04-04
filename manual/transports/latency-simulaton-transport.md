# Latency Simulation Transport

Mirror's Latency Simulation transport allows you to test your project under non-ideal network conditions.

Add it to NetworkManager, **wrap** it around your regular Transport, drag it into NetworkManager.transport.

It can simulate:

* Latency in milliseconds
* Packet loss in %
* Packet scramble / reorder

{% hint style="info" %}
Reliable messages are ordered and guaranteed delivery by definition. Packet loss / scramble over reliable manifests itself via latency.
{% endhint %}

![NMLatencySim](https://user-images.githubusercontent.com/57072365/225437999-0667da1b-abf7-49c5-8c1d-d1a2fec36b12.jpg)
