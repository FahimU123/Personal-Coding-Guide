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

class CountrySinger: Singer {

}


1. Since 
