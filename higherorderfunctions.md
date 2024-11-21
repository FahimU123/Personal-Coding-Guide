# Swift Higher-Order Functions Cheat Sheet

## 1. Transformation Functions

| Function         | Purpose                              | Example Code                               | Result         |
|------------------|--------------------------------------|--------------------------------------------|----------------|
| `map`            | Transform each element.             | `let doubled = nums.map { $0 * 2 }`        | `[2, 4, 6]`    |
| `compactMap`     | Transform & remove `nil`.           | `let valid = arr.compactMap { Int($0) }`   | `[1, 2, 4]`    |
| `flatMap`        | Flatten nested arrays.              | `let flat = arr.flatMap { $0 }`            | `[1, 2]`       |

## 2. Filtering Functions

| Function         | Purpose                              | Example Code                               | Result         |
|------------------|--------------------------------------|--------------------------------------------|----------------|
| `filter`         | Keep elements that match a rule.    | `let evens = nums.filter { $0 % 2 == 0 }`  | `[2, 4]`       |
| `dropFirst`      | Remove first `n` elements.          | `let drop = nums.dropFirst(2)`             | `[3, 4, 5]`    |
| `prefix`         | Keep first `n` elements.            | `let firstTwo = nums.prefix(2)`            | `[1, 2]`       |

## 3. Reducing Functions

| Function         | Purpose                              | Example Code                               | Result         |
|------------------|--------------------------------------|--------------------------------------------|----------------|
| `reduce`         | Combine all into one value.         | `let sum = nums.reduce(0, +)`              | `15`           |
| `reduce(into:)`  | Combine with mutation.              | `let result = nums.reduce(into: 0) { $0 += $1 }` | `15`         |

## 4. Sorting and Rearranging

| Function         | Purpose                              | Example Code                               | Result         |
|------------------|--------------------------------------|--------------------------------------------|----------------|
| `sorted(by:)`    | Sort by a custom rule.              | `let sorted = nums.sorted { $0 < $1 }`     | `[1, 2, 3]`    |
| `reversed`       | Reverse the order.                  | `let reversed = nums.reversed()`           | `[5, 4, 3, 2, 1]` |

## 5. Checking Functions

| Function         | Purpose                              | Example Code                               | Result         |
|------------------|--------------------------------------|--------------------------------------------|----------------|
| `contains`       | Check if the collection contains an element. | `let hasThree = nums.contains(3)`       | `true`         |
| `allSatisfy`     | Check if all elements meet a condition. | `let allPositive = nums.allSatisfy { $0 > 0 }` | `true`     |
| `first(where:)`  | Find the first element matching a condition. | `let firstEven = nums.first { $0 % 2 == 0 }` | `2`         |

## 6. Iteration

| Function         | Purpose                              | Example Code                               | Result         |
|------------------|--------------------------------------|--------------------------------------------|----------------|
| `forEach`        | Perform an action for each item.     | `nums.forEach { print($0) }`               | Prints each element in the array |

---

## **$0 Explained**

In Swift, `$0`, `$1`, `$2`, etc., are shorthand **placeholder names** for the parameters of a closure. When you use these, its just mean your talkking about the first valuie in the array or the second one, etc..

### **Key Points:**
- `$0` refers to **the first argumen/valuet in the array** passed into the closure.
- `$1` refers to **the second argument/value in the array**, and so on.
- This is useful where the closure is simple and doesnt require named parameters.

### **Example with `$0` and `$1`**:

```swift
let numbers = [1, 2, 3, 4]

let doubledNumbers = numbers.map { $0 * 2 }
print(doubledNumbers) // Output: [2, 4, 6]

```

1. Here $0 is going through every value and doubling it and updating the array.
