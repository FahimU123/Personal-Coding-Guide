# Swift Data Structures 

## Array

```swift
  var fruits = ["Apple", "Banana", "Cherry"]

- Access by Index
  `print(fruits[0])  // "Apple"`

  `fruits.append("Orange")`

- **Remove an Item**  
  `fruits.remove(at: 1)`  // Removes "Banana"

  ```

## Dictionary
```swift
- **Create a Dictionary**  
  `var person = ["name": "John", "age": 25]`

- **Access by Key**  
  `print(person["name"]!)  // "John"`

- **Add or Update an Item**  
  `person["city"] = "New York"`

- **Remove an Item**  
  `person.removeValue(forKey: "age")`

- **Iterate over Dictionary**  
  
  for (key, value) in person {
      print("\(key): \(value)")
  }
  ```

## Set
```swift
- **Create a Set**  
  `var numbers: Set = [1, 2, 3, 4]`

- **Add an Item**  
  `numbers.insert(5)`

- **Remove an Item**  
  `numbers.remove(2)`

- **Check if Set Contains Item**  
  `print(numbers.contains(3))  // true`

- **Iterate over Set**  
  ```swift
  for number in numbers {
      print(number)
  }
  ```

## Tuple
```swift
- **Create a Tuple**  
  `var person = ("John", 25)`

- **Access Tuple Elements**  
  `print(person.0)  // "John"`  
  `print(person.1)  // 25`

- **Named Tuple Elements**  
  `var person = (name: "John", age: 25)`  
  `print(person.name)  // "John"`

- **Return Multiple Values from Function**  
  ```swift
  func getPerson() -> (String, Int) {
      return ("John", 25)
  }
  ```
