# Arrays

# Processing Arrays

```


let friends = ["Name", "Name2", "Name3", "Name4", "Name5"]

func invite(friend: String) {
    print("Hey, \(friend), please come to my party on Friday!")
}

invite(friend: friends[0])
invite(friend: friends[1])
invite(friend: friends[2])


```

# Mutuating Arrays

```
var transitOptions = ["walk", "bus", "bike", "drive"]
//: You can assign a whole different array of items:
transitOptions = ["rowboat", "paddle board", "submarine"]


```

# Adding Items

```

var list = [String]()
// You can add a single item using the `append` instance method:
list.append("Banana")

//: You can add an item at a specific index using the `insert` instance method. As with everywhere you use an index, it has to be within the array or the program will crash:
list.insert("Kumquat", at: 0)

//: You can append a whole array of items using the compound assignment operator `+=`:
list += ["Strawberry", "Plum", "Watermelon"]

```

# Removing Items


```

//: The `remove(at:)` method returns the item you have removed:
 
let someNumber = numbers.remove(at: 2)
numbers


//: You can remove the first item using `removeFirst()`:
let firstNumber = numbers.removeFirst()
numbers


//: You can remove the last item using `removeLast()`:
let lastNumber = numbers.removeLast()
numbers

//: Using `removeFirst()` or `removeLast()` on an empty array will cause an error.
You can remove _everything_ using `removeAll()` - this doesn't return anything:

numbers.removeAll()
numbers

```

# Replacing Items

```

var flavors = ["Chocolate", "Vanilla", "Strawberry", "Pistachio", "Rocky Road"]

let firstFlavor = flavors[0] 

//: With a mutable array, you can use the subscript to set the value at an existing index, replacing the value that is already there:


flavors[0] = "Fudge Ripple"

let newFirstFlavor = flavors[0]

```


