In Go können ```structs``` mit string tags annotiert werden.

```
type User struct {
	Username     *string   `bson:"username,omitempty"`
	Password     *string   `bson:"password,omitempty"`
	Token        *Token    `bson:"token,omitempty"`
	Friends      []string  `bson:"friends,omitempty"`
	Profile 	  *Profile   `bson:"profile,omitempty"`
	Role 	       *string   `bson:"role,omitempty"`
}
```

Der ```bson``` tag kann beispielsweise genutzt werden, um dem mongodb Treiber zu sagen, wie mit den struct Feldern umzugehen ist.

Bisher habe ich die durch Thrift generierten ```structs``` vor dem abspeichern in mongo umgewandelt zu eigenen neu definierten ```structs```.
Das alles, weil mongo die string tags braucht.

Aber... Es gibt zum Glück die Möglichkeit in Thrift die ```structs```, die für Go generiert werden vorher zu annotieren.
Beispiel:

```
struct User {
    1: optional string identifier (go.tag = "bson:\"username,omitempty\""),
    3: optional string role,
    4: optional UserProfile profile,
}
```

Wird generiert zu:

```
// Attributes:
//  - Identifier
//  - Role
//  - Profile
type User struct {
	Identifier *string `thrift:"identifier,1" bson:"username,omitempty"`
	// unused field # 2
	Role    *string      `thrift:"role,3" db:"role" json:"role,omitempty"`
	Profile *UserProfile `thrift:"profile,4" db:"profile" json:"profile,omitempty"`
}

```

PERFEKT!
