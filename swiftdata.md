# Swift Data

## 3 Big things 

### Say you have a class called User and you store their name and password in that class, all you have to do above it is type @Model and this tells Swift Data, hey save this stuff
### Make sure in the class you initialize the values
### Also in your main file outside of the WindowGroup you must type  .modelContainer(for: Destination.self, Sight.self), of course, you can replace Destination and  Sight with whatever your Data Model class names were

```swift
@Model
class User {
    var name: String
    var password: String

    init(name: String, password: String) {
        self.name = name
        self.password = password
    }
}


```

```swift
@main
struct iTourApp: App {
    var body: some Scene {
        WindowGroup {
            ContentView()
        }
        .modelContainer(for: Destination.self)
    }
}

```
## @Realtionship

### Use this to link two Data Models that relate to each other

### You get THREE options for deciding how you want to handle related data

1. .cascade - if one of them is deleted so is the other - nukes everything - good for if you want to delete everything.
2. .nullify - if one is deleted the other is still kept BUT THE RELATIONSHIP IS BROKEN NOW - good for if you want to keep related objects but remove the link.
3. .deny - its  safeguard, won't let you delete related data - good for if you want to prevent accidental deletion.
