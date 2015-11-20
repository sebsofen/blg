apache thrift und android würden sich eigentlich gut verstehen.
Wenn da nicht das Problem mit den Annotations wäre.
Thrift generiert nämlich automatisch ```Generated``` annotations, und benötigt dann auch noch ```javax.annotations...```

Das habe ich bisher so umgangen, dass ich die relevanten packages als dependencies in Android Programm hatte.
Oder, indem ich einfach per Hand die Annotations rausgelöscht habe.

Mit diesem Wundervollen [fix](https://github.com/apache/thrift/commit/6e4037656885132a44407fb7d66f6d034b379376), der mitlerweile auch in Thrift gepullt wurde, kann man die Annotations aber direkt bei der Generierung ausschalten.

Dafür braucht man natürlich das neuste Thrift, lässt sich aber mithilfe der [Anleitung](https://github.com/apache/thrift) auf Github Problemlose installieren.

Ein kleiner Blick in die Help:

```
java (Java):
    beans:           Members will be private, and setter methods will return void.
    private-members: Members will be private, but setter methods will return 'this' like usual.
    nocamel:         Do not use CamelCase field accessors with beans.
    fullcamel:       Convert underscored_accessor_or_service_names to camelCase.
    android:         Generated structures are Parcelable.
    android_legacy:  Do not use java.io.IOException(throwable) (available for Android 2.3 and above).
    option_type:     Wrap optional fields in an Option type.
    java5:           Generate Java 1.5 compliant code (includes android_legacy flag).
    reuse-objects:   Data objects will not be allocated, but existing instances will be used (read and write).
    sorted_containers:
                     Use TreeSet/TreeMap instead of HashSet/HashMap as a implementation of set/map.
    undated_generated_annotations:
                     Do not generate the date for the @Generated annotation  javame (Java ME):
```

Ziemlich viel Optionen für java. Eine funktionierende Konfiguration für Android ist:

```
thrift -r --gen java:generated_annotations=suppress  -out ...
```
