# Optionals

```

var nickname: String?

```

1. Here nicnkname can have a value or it can be nil for nothing

```

let publicationYear3: Int? = nil

```

1. This is just more explicit 

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


# If let

```

var numberOfCats: Int? = nil
if let unwrappedNumberOfCats = numberOfCats {
    print("I have \(unwrappedNumberOfCats) cats")
}

```

1. If let is basically if there is a value and its not nil then you can run the code
2. Notice how in the string interpolation I use "unwrappedNumberOfCats" instead of "numberOfCats" because thank to the if let "unwrappedNumberOfCats" has a guaranteed value while "numberOfCats" could potentially be nil


# Guard let

```

let age: Double? = nil
let height: Double? = 45.7


guard let isThereAge = age else {
    fatalError("there was no age")
}

guard let isThereHeight = height else {
    print("enter your height")
    fatalError()
}

let doubleAge = isThereAge * 2
let quarterHeight = isThereHeight / 4

```

1. Guard let is basically making sure there is a vlaue, if no value it will run the code within the guard let block
2. Guard let is just to stop your code from going further because its missing crucial info
3. Guard let requires for you return something, in this example we return a fatalError() but you can do return or throw and this way when you code breaks you can see exactly where it broke


# Force Unwrapping

```

var cranberryJuice: Int? = nil

print(cranberryJuice!)

```

1. Forced unwrapping is recognized via the !
2. It means you are telling the code cranberryJuice WILL have a value no matter what so print it
3. This can be dangerous so be careful

An Example where it does'nt break the code

```

var nameOfDog: "Uncle Dan"

print(nameOfDog!)

```

# If else(Not an official way to unwrap opyionals but it works)

```

let breakfast: String? = "Wheaties"

if breakfast == nil {
        print("Breakfast is the most important meal of the day! When I was your age we...")
} else {
        print("I love \(breakfast!)! Good choice.")
}

```


# Optional Chaniing


```

struct car {
    var year: Int
    var color: String
    var mileage: Int
    var owner: String?
}

struct owner {
    var name: String
    var birthDate: String
    
}

var myCar = car(year: 2017, color: "Black", mileage: 860000, owner: "Fahim")

var fahim = owner(name: "Fahim", birthDate: "July 12")

print(fahim)

```

1. In this code not every car might not have an owner, if they do have a owner, they have a name and birth date
2. After creating two instances I can driectly access owner thank to the fact that owner was an optional


# Optionals and Functions

```

func login(username: String, password: String) {
    print("Hello, \(username), you are logged in!")
    }
 
var username: String? = "DJT"
var password: String? = nil


if let un = username, let pw = password {
    login(username: un, password: pw)
}

```

1. In this example the function doesn't even run before it checks to make sure that THERE is a value inside username and password
