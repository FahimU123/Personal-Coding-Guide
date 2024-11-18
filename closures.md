# Closures

# Basic Closure Without Parameters or Return Value

```

let simpleClosure: () -> () = {
    print("Hello from a closure!")
}
simpleClosure() // Outputs: Hello from a closure!

```

# Closure That Takes Parameters but No Return Value

```

let greet: (String) -> () = { name in
    print("Hello, \(name)!")
}
greet("Fahim") // Outputs: Hello, Fahim!

```

# Closure That Takes Parameters and Returns a Value

```

let add: (Int, Int) -> Int = { (a, b) in
    return a + b
}
print(add(3, 4)) // Outputs: 7

```

# Funcs and Closures

```

func createHighScoreTracker() -> (Int) -> String {
    var highScore = 0  // Initialize the high score to 0

    let tracker: (Int) -> String = { score in
        if score > highScore {
            highScore = score  // Update high score
            return "New high score! Your score is now \(highScore)."
        } else {
            return "Nice try! The high score is still \(highScore)."
        }
    }

    return tracker
}

// Usage
let trackHighScore = createHighScoreTracker()
print(trackHighScore(50))   // "New high score! Your score is now 50."
print(trackHighScore(30))   // "Nice try! The high score is still 50."
print(trackHighScore(100))  // "New high score! Your score is now 100."
print(trackHighScore(90))   // "Nice try! The high score is still 100."

```

1. This is a func which takes no paramaters which returns a closure that takes an Int paramater, which returns a string
2. Always gotta intialize(this is called capturing the value) here because there is no paramter for highScore 
3. tracker is the closure which was referenced in the beginning and takes an Int and returns a string
4. score could be named anything you want and is the paramter in the closure
5. To use you must create an instance



Another Example

```

func add(_ n: Int) -> ((Int) -> Int) {
    let calculate: (Int) -> Int = { (x: Int) in
    return x + n
    }
    return calculate
}


let addOne = add(1)
print(addOne(10))

```

1. x is the paramater in the closure
2. Dont have to initialze here bacuse when the func is called n will always have a value
