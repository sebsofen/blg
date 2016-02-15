Erstmal die SBT dependencies übernehmen:

```
libraryDependencies ++= Seq(

  //TITAN
  //core functionality
  "com.thinkaurelius.titan" % "titan-core" % "1.0.0",
  //cassandra
  "com.thinkaurelius.titan" % "titan-cassandra" % "1.0.0",
  //elastic search
  "com.thinkaurelius.titan" % "titan-es" % "1.0.0",
  
  //STUFF
  //reading config files
  "com.typesafe" % "config" % "1.3.0"
)
```

Es soll TitanDB mit Cassandra und Elastic Search verwendet werden.


