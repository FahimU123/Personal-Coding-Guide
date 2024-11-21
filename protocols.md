# Protocols


```swift

protocol Greet {
  
  var name: String { get }

  func message() 
} 
```
```swift
class Employee: Greet {

  var name = "Perry"

  func message() {
    print("Good Morning", name)
  }
}

var employee1 = Employee()
employee1.message()

```

1. Here a protocol is created that takes a name and a message func
2. Now the class conforms to the Greet protocol, this means class must use both name and message in order to  fully conform
3. This is useful when you have a protocol that can be useful in many structs/classes
4. The get means name has only read permissions. SO in the class name has been set to Perry and CANNOT be changed
5. There is another one whihc is "get set", which means you can read and write, so if name had get set, then we could chnage the value of name.

## Conforming to Multiple Protocols 

```swift

protocol Sum {

  func addition()
}

protocol Multiplication {

  func product()
}

class Calculate: Sum, Multiplication {

  var num1 = 0
  var num2 = 0

  func addition () {
    let result1 = num1 + num2
    print("Sum:", result1)
  }

  func product () {
    let result2 = num1 * num2
    print("Product:", result2)
  }
                   
}

var calc1 = Calculate()


calc1.num1 = 5
calc1.num2 = 10

calc1.addition()
calc1.product()

```

## Protocols Inheriting Protocols

```swift

protocol Car {
  var colorOptions: Int { get }
}

protocol Brand: Car {
  var name: String { get }
}

class Mercedes: Brand {

  var name: String = ""
  var colorOptions: Int = 0
}

var car1 = Mercedes()
car1.name = "Mercedes AMG"
car1.colorOptions = 4

print("Name:", car1.name)
print("Color Options:", car1.colorOptions)

```


## Hashable

```swift

struct Employee: Hashable {
  var name: String
}

let object1 = Employee(name: "Sabby")
let object2 = Employee(name: "Smith")


print(object1.hashValue)
print(object2.hashValue)

```

1. This is a built in protocol by Swift so we can use this in any structure or class we like
2. Hashable creates a unique hash value for the instance


## Equatuable

```swift

struct Person {
    var name: String
    var age: String
}

To make that Equatable you need to add the Equatable conformance like this:

struct Person: Equatable {
    var name: String
    var age: String
}


If you don’t want to check all properties for equality, or if any of your properties are not also Equatable, then you need to write your own == function like this:

static func ==(lhs: Person, rhs: Person) -> Bool {
    return lhs.name == rhs.name && lhs.age == rhs.age
}

```
1. lhs and rhs are what typically used but you can name them anything. They stand for left and right hand side
2. You have to use this static fun to check if both Persons are the same
