# OOP

A way to wirte code whihc models teh rela world. FX app for  ahosputal will have doctor, hospotal, patient, etcc classes

## First: Ecapsulation

This is the rule of not manipulating one classes properties in another class

## Second/Third: Inhertiance/Super methods

Just inherting a parent classes propeties and methods, which can be overwritten 

```swift
class Vehicle {
    var brand: String
    
    init(brand: String) {
        self.brand = brand
    }
    
    func start() {
        print("\(brand) starts up.")
    }
}

class Car: Vehicle {
    var numberOfWheels: Int
    
    /// only need the super init if you have a new uninitiazed  property or if u explicity write a cutom init even if u have a default value
    init(brand: String, numberOfWheels: Int) {
        /// must ALWAYS inilize the current classes properties then parents
        self.numberOfWheels = numberOfWheels
        super.init(brand: brand)
    }
    
    /// if your instance happnes to be  vehihcle which is a car itll perform the action here
    override func start() {
        super.start()
        print("The \(brand) car engine roars!")
    }
    
    /// can ofc add new properties and method liek here
    func drive() {
        print("The \(brand) car is driving on \(numberOfWheels) wheels.")
    }
}
```

## Fourth: Polymorphism(Many Forms)

Imagine you have a "talk" button.

If you press the "talk" button on a dog, it barks.

If you press the "talk" button on a cat, it meows.

If you press the "talk" button on a human, they speak words.

The action (pressing "talk") is the same, but the result is different depending on what you pressed it on.

```swift
protocol Drawable {
    func draw()
}

class Circle: Drawable {
    func draw() {
        print("Drawing a circle")
    }
}

class Rectangle: Drawable {
    func draw() {
        print("Drawing a rectangle")
    }
}

class Star: Drawable {
    func draw() {
        print("Drawing a star")
    }
}

let allShapes: [Drawable] = [Circle(), Rectangle(), Star()]

for shape in allShapes {
    shape.draw() // Each shape knows how to draw itself!
}
```

# Fifth: Final classes

Disables inheritance but slight peorformance benfit since Scode doesnt have to do extra checks for inheritance, can also mark individual properties and methods final to enforce design contriants so youd ont modify imoportnat behavior elsewhere

