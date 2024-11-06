# Optionals

```

var nickname: String?

```

1. Here nicnkname can have a value or it can be nil for nothing

```

let publicationYear3: Int? = nil

```

1. This is juys more explicit 

```

struct Person {
    var firstName: String
    var lastName: String
    let birthYear: Int
    let starSign: String
    let bnaiMitzvahDate: String?
    var age: Int
    var glassesPrescription: Double?
}

```
1. Even in structs theres optionals(they are everywhere)

# Nil Coalescing

```

var name: String = "Ivoire"
var nickname: String? = "Ivy"
print("Hello, \(nickname ?? name)")

```
1. In the print statemnet is, where it has the nil coalescing, it wil print nickname if it has a value otherwise it will print whatver is in the name var
2. Nil coalescing is just a way for your code to have a backup so it doesnt crash if it doenst have a value

Another example

```

var numbers = [1, 2 ,3 ,4, 5]
print(numbers.max() ?? 5)

```
