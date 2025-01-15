# Error Handling


```swift
enum MathError: Error {
    case divisionByZero
}

func divide(_ a: Int, by b: Int) throws -> Int {
    if b == 0 {
        throw MathError.divisionByZero
    }
    return a / b
}

do {
    try divide(10, by: 0)
} catch {
    print("An error occurred: \(error)")
}

```
1. this just a normal func , and throws just makes it capable of throwing errors
2. do basically means, yo do this
3. Try means, yo ths might throw an error
4. catch is basically if you do get an erorr, that is what you will do in the catch block
