
# Lazy Properties

these are only intialzed when they are asked for, good for heavy tasks, liek network request, filtering image

```swift
class Greeter {
    let perosnName: String
    
    init(perosnName: String) {
        self.perosnName = perosnName
    }
    
    /// yes the say the explict type and yes have the () after the last }
    lazy var welcomeMessage: String = {
        "hello \(self.perosnName)"
    }()
}
```

                                                    
## this just the much cleaenr wya to do it


```swift
class Greeter {
    let perosnName: String
    
    init(perosnName: String) {
        self.perosnName = perosnName
    }
    
    private func generateWelcomeMessage() -> String {
        "Hello, \(self.perosnName)! Welcome to the app."
    }
    
    /// this is cleaner, do this!
    lazy var welcomeMessage: String = self.generateWelcomeMessage()
}


let greet = Greeter(perosnName: "fahim")
print(greet.welcomeMessage)


