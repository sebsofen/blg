Eine existierende TitanDB Instanz soll visualisiert werden.

Dateiformat für Connection!
http://s3.thinkaurelius.com/docs/titan/0.5.0/titan-io-format.html

Zum Beispiel so:

```
storage.backend=cassandra
storage.hostname=127.0.0.1

index.search.backend=elasticsearch
index.search.hostname=127.0.0.1
```

Laden:

```
TitanFactory.open("/home/sebastian/Desktop/titandb-connect")
```

Für lokale installation.

der Export in Gremlin gestaltet sich dann wie folgt:

```
gremlin> graph = TinkerFactory.createModern()
==>tinkergraph[vertices:6 edges:6]
gremlin> graph.io(IoCore.graphml()).writeGraph("/home/sebastian/tinkerpop-modern.graphml");
==>null
gremlin> 
```
Auf die korrekte Dateiendung ist zu achten!

In Gephi kann man den Spaß dann easy peasy importieren und visualisieren:

![Alt text](titan_visualisation/Selection_001.jpg "6 nodes 6 vertices Visualisierung")
