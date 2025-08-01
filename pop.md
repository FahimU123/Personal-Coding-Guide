# POP
## Enourages the thinking of Has A vs. Is A. Defines behavior instead trying to model an entity. POP provides default implentation throgh extensions

# Protocol Extensions

```swift

// 1. Define the Protocol: What core behavior must a 'Describable' thing have?
protocol Describable {
    /// Properties in protocols must have  a get, set or BOTH
    var descriptionText: String { get } // REQUIRED: Every describable must have a description
    func describeSelf()                 // REQUIRED: Every describable must be able to describe itself
}

// 2. Protocol Extension: Provide default behavior and new utility methods

// This extension provides a default implementation for the REQUIRED 'describeSelf()' method
extension Describable {
    func describeSelf() {
        print("Default Description: \(descriptionText)")
    }
    
    // This is a NEW method 'logDescription()' that is NOT a protocol requirement.
    // It's a common utility shared by all Describables through the extension.
    func logDescription() {
        print("LOG: [\(Date())] -- \(descriptionText)")
    }
}

// 3. Conforming Types: Adopt the protocol and optionally customize behavior

// Type A: Book (a struct) - Conforms and uses default behavior
struct Book: Describable {
    let title: String
    let author: String
    
    // Fulfills the 'descriptionText' requirement
    var descriptionText: String {
        return "'\(title)' by \(author)"
    }
    // 'Book' will automatically get the default behavior from the protocol extension.
}

let hobbit = Book(title: "The Hobbit", author: "J.R.R. Tolkien")
hobbit.describeSelf()   // Output: Default Description: 'The Hobbit' by J.R.R. Tolkien AKA the default implentation
hobbit.logDescription() // Output: LOG: [Timestamp] -- 'The Hobbit' by J.R.R. Tolkien AKA the default implentation


// Referring to it as the Describable gives it the output of the extensions not any custom function if you ahd any in the struct itself
let myBookAsDescribable: Describable = Book(title: "1984", author: "George Orwell")
myBookAsDescribable.describeSelf()   // Output: Default Description: '1984' by George Orwell
myBookAsDescribable.logDescription() // Output: LOG: [Timestamp] -- '1984' by George Orwell

// Type B: Pet (a class) - Conforms and customizes behavior
class Pet: Describable {
    var name: String
    var species: String
    
    init(name: String, species: String) {
        self.name = name
        self.species = species
    }
    
    // Fulfills the 'descriptionText' requirement
    var descriptionText: String {
        return "\(name) the \(species)"
    }
    // Custom Implemntation
    func describeSelf() { // Custom implementation for the REQUIRED 'describeSelf()' method
        print("I am \(name), a \(species).")
    }
    
    // This is a custom implementation for the EXTENSION-ONLY 'logDescription()' method.
    // Important: This will ONLY be called if you use the concrete type (Pet),
    // NOT if you treat it as a 'Describable' protocol type for this method.
    func logDescription() {
        print("CUSTOM LOG FOR PET: It's \(name)!")
    }
}

let fluffy = Pet(name: "Fluffy", species: "cat")
// Both of these get the custom implemtnation because of how the intance was craeted, It is a pet first not of type Describale
fluffy.describeSelf()   // Output: I am Fluffy, a cat.
fluffy.logDescription() // Output: CUSTOM LOG FOR PET: It's Fluffy!



// Creating a 'Pet' instance, but referring to it as 'Describable'
let myPetAsDescribable: Describable = Pet(name: "Buddy", species: "dog")
// Even though descirbeSelf has a default implentation, since its a required method within the Protocol, the FUNCTIONALITY itself can be overwirtten to anyone who conforms to it
myPetAsDescribable.describeSelf()   // Output: I am Buddy, a dog. (Pet's custom implementation)
// (This is the crucial part: it calls the PROTOCOL EXTENSION'S logDescription,
// NOT Pet's custom one, because 'logDescription' is not a protocol requirement!)
myPetAsDescribable.logDescription() // Output: LOG: [Timestamp] -- Buddy the dog
```

# POP in PRAC

```swift
protocol Payable {
    func claculateWages() -> Int
}

extension Payable {
    func claculateWages() -> Int {
        10_000
    }
}

protocol ProvidesTreatemnt {
    func treat(name: String)
}

extension ProvidesTreatemnt {
    func treat(name: String) {
        print("Treade \(name)")
    }
}

protocol ProvideDiagnosis {
    func diagnose() -> String
}

extension ProvideDiagnosis {
    func diagnose() -> String {
        ("Hes dead")
    }
}

protocol COnductSurgery {
    func performSuregry()
}

extension COnductSurgery {
    func performSuregry() {
        print("success")
    }
}

protocol HasRestTime {
    func takeBreak()
}


extension HasRestTime {
    func takeBreak() {
        print("lets watch TV")
    }
}


protocol NeedsTraingin {
    func study()
}


extension NeedsTraingin {
    func study() {
        print("reading a book")
    }
}

protocol Employee: Payable, HasRestTime, NeedsTraingin {  }

struct Receptionist {
    
}

extension Receptionist: Employee { }

struct Nurse {
    
}

extension Nurse:Employee, ProvidesTreatemnt { }


struct Doctor {
    
}

extension Doctor: Employee, ProvidesTreatemnt, ProvideDiagnosis { }


struct Surgeon {
    
}

extension Surgeon: Employee, COnductSurgery, ProvideDiagnosis { }



```

# Protoxol Constraint Extenisions 

```swift
protocol EMployee { }

// This function is only availible to types who conform to employee and ProvidesTreatment protocol
extension EMployee where Self: ProvidesTreatment {
    func checkInsurance() {
        print("Insured")
    }
}

protocol ProvidesTreatment { }


// Element is each item ina collection,BinaryInteger is just bunch of differnet number types, returns a tuple, self referring an instnce of Collection
extension Collection where Element: BinaryInteger {
    func countOddandEVen() -> (odd: Int, even: Int) {
        var even = 0
        var odd = 0
        
        for val in self {
            if val.isMultiple(of: 2) {
                even += 1
            } else {
                odd += 1
            }
        }
        return (odd, even)
    }
}

```
