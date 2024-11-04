# Functions


# Functions that call on other Functions



```

func sailorWentToSea() {
    print("A sailor went to sea, sea, sea")
}


func toSeeWhatHeCouldSee() {
    print("What he could see, see , see")
}

func butALlThatHeCouldSee() {
    print("But all tha he could see, see, see")
}

func wasTheBottomOfTheSea() {
    print("Was the bottom of the sea, sea, sea")
}

func aSailorWentToSea() {
    sailorWentToSea()
    toSeeWhatHeCouldSee()
    butALlThatHeCouldSee()
    wasTheBottomOfTheSea()
}

aSailorWentToSea()

```

Another Example

```

func wheelsOnTheBus() {
    print("The wheels on the bus go round and round")
}


func roundAndround() {
    print("round and round")
}

func allThroughTheTown() {
    print("All through the town")
}

func verseOne(){
    wheelsOnTheBus()
    roundAndround()
    roundAndround()
    allThroughTheTown()
}

verseOne()

```

# Basic Paramaters

Passing one value

```

func hello(name: String) {
    print("Hello " + name)
}

```

```

hello(name: "Maria")

```
Passing 2 values

```

func hello(firstName: String, lastName: String) {
    print("Hello \(firstName) \(lastName)")
}

```

```

hello(firstName: "Johnny", lastName: "Appleseed")
hello(firstName: "John", lastName: "Snow")

```

# Returning Values

```

func repsAndSetsOfCurls(reps: Int, sets: Int) -> String{
  
    
    let totalCurls = reps * sets
    
    return "You did \(totalCurls) curls"
}

```

```

let total = repsAndSetsOfCurls(reps: 2, sets: 10)

print(total)

print(repsAndSetsOfCurls(reps: 5, sets: 10))

```

1. The arrow means you're returning something so thereofre you MUST return something in your code block.
2. Instead of regularly just calling funcs you must set it to a constant and then print that constant
3. You can also do the 2nd print statemnt shown in the example above

# More Complex Returning 

```

func listByAdding(item: String, toList: String) -> String {
    return toList + "\n" + item
}
var list = ""
list = listByAdding(item:"Eggs", toList: list)
list = listByAdding(item:"Bread", toList: list)

list += "\n" + "Rice"

print(list)

```

1. List is techinically an empty string

Similiar Example 

```

func listByAdding(item: String, toList: String) -> String {
    let newList = toList + "\n- " + item
    return newList
}

var list = ""
var numberOfItems = 0

list = listByAdding(item:"Milk", toList: list)
numberOfItems += 1
list = listByAdding(item:"Eggs", toList: list)
numberOfItems += 1
list = listByAdding(item:"Bread", toList: list)
numberOfItems += 1

print("Your shopping list contains \(numberOfItems) items:\(list)")

```

# Function Readability

```

func printHello(to name: String) {
    print("Hello " + name)
}

func printHi( _ name: String) {
    print("Hi " + name)
}


printHello(to: "Chris")
printHi("Johnny")

```

1. The first word in the paramater can be anything and people usually have it for readability
2. There is one example that says "to" and the other is just an  _  and you can see that affects the print statements

# More Good Examples of Functions

```

func openingLine(_ verb: String, _ noun: String) {
    print("\(verb), \(verb), \(verb), your , \(noun)")
    
}

openingLine("row", "Boat")

```

```

func holler(_ phrase: String) -> String {
    return "⚡️\(phrase)!!⚡️"
}

holler("Thank you, this is very nice.")

```
