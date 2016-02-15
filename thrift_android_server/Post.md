Idee
--------
Das Bild erklärt die Idee eigentlich schon sehr gut:
Es soll der Datenaustausch zwischen Android Smartphone und Desktop vereinfacht werden.
Dabei ist erstmal der Ansatz, Daten vom Desktop *an das* Smartphone zu schicken, nicht umgekehrt (das könnte man aber auch später nochmal überlegen).

Die Dateiübertragung soll für den Nutzer möglichst umkompliziert und direkt erscheinen.
Deshalb soll die Desktop Applikation Dateien und Text per Drag and Drop entgegennehmen, diese an das Smartphone schicken und dort ein *Share Intent* auslösen, mit dem dann direkt die gewünschte App geöffnet werden kann, die die Daten erhalten soll.

Somit werden kompliziertere Zwischenstopps, wie Dropbox, irgendwelche Messenger oder so übergangen.


![idd](thrift_android_server/dragndrop.jpg "Drag and Drop Files aufs Smartphone")
Übertraungsservice
-----------
Herzstück der Applikation ist ein Thrift Server, der die Datenübertragung zwischen den Geräten ermöglicht. Der Server läuft hierbei auf der App, sobald diese gestartet wird.

```
namespace java  sebastians.intentapp.networking

enum DataType {
  IMAGE,
}

struct TransferIntent {
  1: required i32 chunkcount,
  2: required DataType datatype,
}

struct Chunk {
  1: required i32 intentid,
  2: required binary data,
  3: required i32 chunkid,
}

service TransferSvc {
  i32 announceTransferIntent(1: TransferIntent intent);
  void sendChunk(1: Chunk chunk);
}

```



Das vorläufige Ergebnis: Der Thrift Server läuft auf dem Android Gerät!


```

Nmap scan report for android-46c61c850994645b.fritz.box (192.168.178.81)
Host is up (0.013s latency).
Not shown: 999 closed ports
PORT     STATE SERVICE
7911/tcp open  unknown

```

TODO
===============

Identifikation der Gerätable
---------------
Ursprünglich kennt die Desktop Applikation die IP des Smartphones (im Netzwerk) nicht.
Hier gibt es einige Ansätze, die man verfolgen könnte, um die beiden Geräte miteinander bekannt zu machen.

- der Desktop verfügt auch über einen server und zeigt die ip als qr code -> die app scant den code -> ruft funktion auf desktop auf und teilt so die ip mit
- die app zeigt die aktuelle ip in der activity -> manuelle eingabe auf dem desktop
- die desktop app scannt alle verfügbaren ips nach dem offenen port für die datenübertragung
- ...

Datenübertragung
----------------

Ich teile große Files in konsumbare Chunks, damit die App nicht einfriert, und ein Übertragungsprozess angezeigt werden kann.
Sobald alle Chunks überreicht wurden, beginnt die App, die Chunks wieder neu zusammen zu setzen.
Dabei kommt es aber im Moment noch zu einem Heap Overflow, wenn die Files zu groß sind.

```
Throwing OutOfMemoryError "Failed to allocate a 96000012 byte allocation with 16777120 free bytes and 84MB until OOM"
```

![overflow](thrift_android_server/memory_error.png "Memory Usage der Android App")

Drag and Drop
--------------
auf desktopebene muss eine gui applikation her, die möglichst auch den übertragungsstatus anzeigen kann, und daten per drag and drop empfängt.
- http://stackoverflow.com/questions/811248/how-can-i-use-drag-and-drop-in-swing-to-get-file-path
