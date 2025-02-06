# Code Design

## When to use Functions

### Signs:

1. Youre repeating code
2. Your function is very long and handling many tasks

## When to use Structs or Classes

### Signs:

1. you need to group related data, for example you han have 3 constants of first name, last name, BDAY, but since tahts all related to a user you cna have a strcut or a class User
2. If the data you want to store, you also want to perfrom actions on that data.

   ```swift
   struct BankAccount {
    var balance: Double
    
    mutating func deposit(amount: Double) {
        balance += amount
    }
    
    mutating func withdraw(amount: Double) {
        if balance >= amount {
            balance -= amount
        } else {
            print("Insufficient funds!")
        }
    }
    }


## When to use protocols

### Signs:

1. If you wnat to ensure consistency

```swift
protocol Powerable {
    func turnOn()
    func turnOff()
}

class Laptop: Powerable {
    func turnOn() {
        print("Laptop is turning on.")
    }
    
    func turnOff() {
        print("Laptop is turning off.")
    }
}
```

  

