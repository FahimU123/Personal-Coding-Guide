# Structs


## Memberwise Initializer

```swift

struct Song {
    let title: String
    let artist: String
    let duration: Int
}

```

### Once you’ve declared a new type, you can create an instance like this:

```swift

let song = Song(title: "No, no, no", artist: "Fizz", duration: 150)

```


### In the example above, song is an instance of Song, and Song is the type. Each property can be accessed like this:


```swift

song.title
song.artist
song.duration
```
```

### Now since the data structure is now a data type you cna write function like this: 

```swift

func songInformation(song: Song) -> String {
    return "This songs name is  \(song.title), and its by \(song.artist), and its \(song.duration) seconds long"
}

```

1. The song paramater only exists in that funtiopn and again the data type is the struct
2. To access the properties of Song, you must use . notation along with the var you created within that function


## Computed Properties


#### Example 1

```swift

struct Song {

    let title: String
    let artist: String
    let duration: Int
    
    var formattedDuration: String {
        let minutes = duration / 60
        // The modulus (%) operator gives the remainder
        let seconds = duration % 60
        return "\(minutes)m \(seconds)s"
    }
    
    var formattedTitle: String {
        return "\(title) by \(artist)"
    }
    
    func songInformation(song: Song) -> String {
        return "This songs name is  \(song.title), and its by \(song.artist), and its \(song.duration) seconds long"
    }

    
}

let song = Song(title: "No, no, no", artist: "Fizz", duration: 150)

print(song.formattedDuration)

print(song.formattedTitle)

print(song.songInformation(song: song))

````


#### Example 2


```swift


struct Rectangle {
    let width: Int
    let height: Int

    func isAreaLarger(than rectangle: Rectangle) -> Bool {
      let areaOne = height * width
      let areaTwo = rectangle.height * rectangle.width
      return areaOne > areaTwo
    }
}

```

```swift

let rectangle = Rectangle(width: 10, height: 10)
let anotherRectangle = Rectangle(width: 10, height: 30)

regctangle.isAreaLarger(than: anotherRectangle)

isRectangle(rectangle, than: anotherRectangle)


```

1. Each rectangle has a width, a height, and a function to check if it's own area is larger than a different rectangle's area that we pass in

2. Create an instance of a Rectangle called rectangle (and another instance of a Rectangle called anotherRectangle)

3. Use dot notation to access the method isLargerThan and compare it to another rectangle we pass in as a parameter


#### Example 3

```swift

struct Rectangle {
    let width: Int
    let height: Int
    
    
    func isAreaLargerThan(_ rectangle: Rectangle) -> Bool {
        return area > rectangle.area
    }
    
    var area: Int {
        return width * height
    }
}


```

```swift

let rectangle = Rectangle(width: 10, height: 10)
let otherRectangle = Rectangle(width: 10, height: 20)

rectangle.isAreaLargerThan(otherRectangle)

```

1. Samething but doing the area computation outaide of the function
2. The first area in return statement is comparing it to its self and to compare the second one you must do the paramaters var and do dot notation to compuatate area

```swift

func isLongerThan(_ song: Song) -> Bool {
        return duration > song.duration

```

```swift

var longestSong = songs[1]

for song in songs {
    if song.isLongerThan(longestSong) {
        longestSong = song
    }

````
1. For the same struct if this func is in the structure it will calculate which song is longer
2. Firstly it will compare to its self then to compare the second one you must do the paramaters var and then do dot notation
3. Then create var to hold the current song to compare to every other song
4. The for loop goes through every song in the songs arrray and compare it and if its longer then it will be the new value of longestSong


## Custom Initializers

```swift

struct Height {
    var heightInches: Double
    var heightCentimeters: Double
    
    
    init(heightToInches: Double) {
        self.heightInches = heightToInches
        self.heightCentimeters = heightInches * 2.54
    }
    
    init(heightToCentimeters: Double) {
        self.heightCentimeters = heightToCentimeters
        self.heightInches = heightCentimeters / 2.54
    }
}

let heightConvert = Height(heightToInches: 44)
let centimeterConvert = Height(heightToCentimeters: 55)

print(heightConvert)
print(centimeterConvert)


```

1. The left side on inits is the var under the struct
2. The right side on the inits is the paramater var
3. With custom inits you set a default value and that can be computated like this one to turn inches to heights and vice versa, this makes the code dynamic

#### Another Example 


```swift

struct Distance {
    var meters: Double
    var feet: Double
    
    
    init(meters: Double) {
        self.meters = meters
        self.feet = meters * 3.28084
        
    }
    
    init(feet: Double) {
        self.feet = feet
        self.meters = feet * 0.3048
        
    }
    
}

```

## Methods

```swift

struct Book {
    var title: String
    var author: String
    var pages: Int
    var price: Double
    
    func description() {
        print("Title: \(title)")
        print("The author is: \(author)")
        print("Pages: \(pages)")
        print("Price: \(price)")
    }
}


var myBook = Book(title: "S", author: "s", pages: 87, price: 77)

myBook.description()


```

1. Methods are function that do actions in the struct

#### Example with a mutating func


```swift


struct Steps {
    var steps: Int
    var goal: Int
    
    mutating func takeSteps() {
        steps += 1
    }
    
}

var takeStep = Steps(steps: 232, goal: 250)

takeStep.takeSteps()

print("Steps: \(takeStep.steps), Goal: \(takeStep.goal)")


```

## didSet

```swift

struct Height {
    var heightInInches: Double {
        didSet {
            let calculatedHeightInCentimeters = heightInInches * 2.54
            if heightInCentimeters != calculatedHeightInCentimeters {
                heightInCentimeters = calculatedHeightInCentimeters
            }
        }
    }
    
    var heightInCentimeters: Double {
        didSet {
            let calculatedHeightInInches = heightInCentimeters / 2.54
            if heightInInches != calculatedHeightInInches {
                heightInInches = calculatedHeightInInches
            }
        }
    }
    
    init(heightInInches: Double) {
        self.heightInInches = heightInInches
        self.heightInCentimeters = heightInInches * 2.54
    }
    
    init(heightInCentimeters: Double) {
        self.heightInCentimeters = heightInCentimeters
        self.heightInInches = heightInCentimeters / 2.54
    }
}


var height = Height(heightInInches: 70)
print("Initial height: \(height.heightInInches) inches, \(height.heightInCentimeters) cm")


height.heightInInches = 72
print("Updated height: \(height.heightInInches) inches, \(height.heightInCentimeters) cm")


height.heightInCentimeters = 180
print("Updated height: \(height.heightInInches) inches, \(height.heightInCentimeters) cm")

```

1. didSet is used to react to changes
2. When and only when height in centimeters/inches CHANGES the the code in that computed property will run



## willSet

```swift

struct Steps {
    var steps: Int {
        willSet {
            if newValue == goal {
                print("Nice")
            }
            else {
                print("Not yet")
            }
        }
    }
    var goal: Int
    
    mutating func takeStep() {
        steps += 1
    }
}

var test = Steps(steps: 9, goal: 10)

```

1. willSet is for preparing for chnges.
2. willSet is like a heads-up for when a property is about to change, giving you a chance to act on the incoming value.
3. The Steps struct tracks steps toward a goal. When steps is about to change:
4. If steps == goal (like reaching 10): It prints "Nice". Otherwise: It prints "Not yet".



## Static


Use static when you need a shared, class-level variable or function.
Use instance variables for data that should be unique to each object.

#### Static Var


```swift

class AppSettings {
    static var appVersion = "1.0"  // Same for everyone
}
print(AppSettings.appVersion)  // Outputs: 1.0

```

```swift


struct User {
    var userName: String
    var email: String
    var age: Int
    
    static var currentUser: User?
}


let me = User(userName: "FahimUddin", email: "fahim@example.com", age: 20)


User.currentUser = me


if let currentUser = User.currentUser {
    print("Current User:")
    print("Username: \(currentUser.userName)")
    print("Email: \(currentUser.email)")
    print("Age: \(currentUser.age)")
} else {
    print("No user is currently logged in.")
}

```

1. Static means it can be accessed indepenently without an instance, you can just use the dot notaion shown above
2. The ? basically means User can have a value or it can be nil(nothing)
3. If let is used for if user does happen to have value, it will run that code(fancy term: unwrapping an optional)


#### Static Func

```swift

struct RunningWorkout {
    var distance: Double
    var time: Double
    var elevation: Double
    
    static func mileTimeFor(distance: Double, time: Double) -> Double {
        let miles = distance / 1600
        return time / miles
    }
}

let requiredMileTime = RunningWorkout.mileTimeFor(distance: 3200, time: 30)
print("Required mile time: \(requiredMileTime) minutes per mile")


```

1. Same as above, you can access the func with dot notation since its static
2. This static func would be the same for everyone hence the static keyword

