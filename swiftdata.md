# Swift Data - Refer to Paul Hudsons iTour for a full look at an app that uses Swift Data

## 3 Big things 

### Say you have a class called User and you store their name and password in that class, all you have to do above it is type @Model and this tells Swift Data, hey save this stuff
### Make sure in the class you initialize the values
### Also in your main file outside of the WindowGroup you must type  .modelContainer(for: Destination.self, Sight.self), of course, you can replace Destination and Sight with whatever your Data Model class names were

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

```swift

 @Relationship(deleteRule: .cascade) var tasks: [Task] = []

```

So that's the synatx for a relationship, you can of course replace .cascade with whatever you choose and tasks, well that can be whatever you choose to make a relationship with

## @Query

### Now at this point you have data, so you can fetch it, once you grab the data, you can sort it however you like, with #PREDICATE or .searchable you can even filter 
### And now you can display that data after having fetched it the way you wanted it displayed
### Predicate is more complex but more customizable, .seachable should suffice

```swift

@Query(sort: \Destination.name)
```

So that's some syntax that fetches the data in alphabetical order

## .searchable

```swift
struct ContentView: View {
    let names = ["Holly", "Josh", "Rhonda", "Ted"]
    @State private var searchText = ""

    var body: some View {
        NavigationStack {
            List {
                ForEach(searchResults, id: \.self) { name in
                    NavigationLink {
                        Text(name)
                    } label: {
                        Text(name)
                    }
                }
            }
            .navigationTitle("Contacts")
        }
        .searchable(text: $searchText)            
    }

    var searchResults: [String] {
        if searchText.isEmpty {
            return names
        } else {
            return names.filter { $0.contains(searchText) }
        }
    }
}
```
## Adding, Deleting, Updating, Saving Data

### You only need model context in a file when saving, adding, removing, or updating

```swift

 @Environment(\.modelContext) var modelContext
```

```swift

.toolbar {
    Button("Create", action: create)
    Button("Save") {
        try? modelContext.save()
                }
            }

```

And of course for the other situations, its `modelConext.insert`, .remove, I think, you can google it


