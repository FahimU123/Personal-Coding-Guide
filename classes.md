# Classes

```
class Person {
    var clothes: String
    var shoes: String

    init(clothes: String, shoes: String) {
        self.clothes = clothes
        self.shoes = shoes
    }
}

```

1. If a paramater does not have a default value, you must initialize the with init


# Class Inheritance

```

class Singer {
    var name: String
    var age: Int

    init(name: String, age: Int) {
        self.name = name
        self.age = age
    }

    func sing() {
        print("La la la la")
    }
}


```

```

class CountrySinger: Singer {
    override func sing() {
        print("Trucks, guitars, and liquor")
    }
}

```

1. CountrySinger is a subclass and it has inherited every property/method of Singer
2. The override keyword allows the the function to be changed


```

class HeavyMetalSinger: Singer {
    var noiseLevel: Int

    init(name: String, age: Int, noiseLevel: Int) {
        self.noiseLevel = noiseLevel
        super.init(name: name, age: age)
    }

    override func sing() {
        print("Grrrrr rargh rargh rarrrrgh!")
    }
}


```

1. This is a subclass of singer
2. Since this subclass has an extra property called noiseLevel and it doesnt have a default value, it must be intialized
3. Intializing is a little differnt in a subclass, refer to syntax in the example above to see how


# Value vs References

Value Type: When you make a copy of something it becomes independent. It doenst affect your orginial code. For example you pass around a sticky notes with the same stick drawing and your friend chages his.

Reference Type: When you make a copy of something, everyone is still looking at the same original thing. ANy chnages effect the original code. For exmaple, you and your freind look at a whiteboard with a stick figure and he erases a hand


Conclusion: In short value types, when you make a copy, the copy doesnt affect the orginal code, reference types however ar the opposite, they will affect the original code


