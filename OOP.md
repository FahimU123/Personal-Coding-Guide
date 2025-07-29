# OOP

A way to wirte code whihc models teh rela world. FX app for  ahosputal will have doctor, hospotal, patient, etcc classes

## First: Ecapsulation

This is the rule of not manipulating one classes properties in another class

## Second: Inhertiance

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


