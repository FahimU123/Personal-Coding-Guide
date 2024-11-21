# Swift Data Structures 

# Simple Ones First

## Array

```swift
  var fruits = ["Apple", "Banana", "Cherry"]

- Access by Index
  print(fruits[0])  // "Apple"

  fruits.append("Orange")

- Remove an Item
  fruits.remove(at: 1)`  // Removes "Banana"

  ```

## Dictionary
```swift
- Create a Dictionary  
  var person = ["name": "John", "age": 25]

- Access by Key  
  print(person["name"]!)  // "John"

- Add or Update an Item  
  person["city"] = "New York"

- Remove an Item  
  person.removeValue(forKey: "age")

- Iterate over Dictionary  
  
  for (key, value) in person {
      print("\(key): \(value)")
  }
  ```

## Set
```swift
- Create a Set  
  var numbers: Set = [1, 2, 3, 4]`

- Add an Item  
  numbers.insert(5)`

- Remove an Item  
  numbers.remove(2)

- Check if Set Contains Item  
  print(numbers.contains(3))  // true

- Iterate over Set
  for number in numbers {
      print(number)
  }
  ```

###  Sets store unique values and automatically eliminate duplicates.

## Tuple
```swift
- Create a Tuple  
  var person = ("John", 25)

- Access Tuple Elements  
  print(person.0)  // "John"  
  print(person.1)  // 25`

- Named Tuple Elements  
  var person = (name: "John", age: 25) 
  print(person.name)  // "John"`

- Return Multiple Values from Function  
 
  func getPerson() -> (String, Int) {
      return ("John", 25)
  }
  ```
### Tuples group different types of values together.

# More Complex Data Structures


## Stacks 

### In stacks it all about the last in first out rule
### This means the last item you add to the stack is the first one to be removed.

#### Use Cases :  For tasks where you need to go back to the previous state, like undo, or navigating back in a web browser.

```swift

class Stack {
    var items: [Int] = []  // Array to hold stack items
    
    // Push: Add an item to the stack
    func push(_ item: Int) {
        items.append(item)
    }

    // Pop: Remove the top item from the stack and return it
    func pop() -> Int? {
        return items.popLast()  // popLast() removes and returns the last item from the array
    }
    
    // Peek: Return the top item without removing it
    func peek() -> Int? {
        return items.last  // Return the last item without removing it
    }

    // isEmpty: Check if the stack is empty
    func isEmpty() -> Bool {
        return items.isEmpty  // Checks if the array has no elements
    }
}

```


1. `.popLast` is very similair to `.removeLast` BUT  `.popLast` is safer because it returns an optional, meaning you can handle the case of an empty array gracefully.

### Example Usage of the Code Above

```swift

let stack = Stack()

stack.push(10)  // Adds 10 to the stack
stack.push(20)  // Adds 20 to the stack
stack.push(30)  // Adds 30 to the stack

print(stack.peek()!)  // 30 (Top of the stack)

stack.pop()  // Removes 30 from the stack
print(stack.peek()!)  // 20 (Top of the stack)

print(stack.isEmpty())  // false (Stack is not empty)

```
1. MUST USE `.push` as it relates to stacks exclusively, `.append` is for arrays
