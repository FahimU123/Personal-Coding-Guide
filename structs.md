# Structs


# Creating a basic struct

```

struct Song {
    let title: String
    let artist: String
    let duration: Int
}

```

Once you’ve declared a new type, you can create an instance like this:

```

let song = Song(title: "No, no, no", artist: "Fizz", duration: 150)

```


In the example above, song is an instance of Song, and Song is the type. Each property can be accessed like this:


```

song.title
song.artist
song.duration

```

Now since the data structure is now a data typoe you cna write function like this: 

```

func songInformation(song: Song) -> String {
    return "This songs name is  \(song.title), and its by \(song.artist), and its \(song.duration) seconds long"
}

```

1. The song paramater only exists in that funtiopn and again the data type is the struct
2. To access the properties of Song, you must use . notation along with the var you created within that function


# Computed Properties


Example 1

```

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


Example 2


```


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

```

let rectangle = Rectangle(width: 10, height: 10)
let anotherRectangle = Rectangle(width: 10, height: 30)

regctangle.isAreaLarger(than: anotherRectangle)

isRectangle(rectangle, than: anotherRectangle)


```

1. Each rectangle has a width, a height, and a function to check if it's own area is larger than a different rectangle's area that we pass in

2. Create an instance of a Rectangle called rectangle (and another instance of a Rectangle called anotherRectangle)

3. Use dot notation to access the method isLargerThan and compare it to another rectangle we pass in as a parameter


Example 3

```

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

```

let rectangle = Rectangle(width: 10, height: 10)
let otherRectangle = Rectangle(width: 10, height: 20)

rectangle.isAreaLargerThan(otherRectangle)

```

1. Samething but doing the area computation outaide of the function
2. The first area in return statement is comparing it to its self and to compare the second one you must do the paramaters var and do dot notation to compuatate area

```

func isLongerThan(_ song: Song) -> Bool {
        return duration > song.duration

```

```

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


# Custom Initializers

```

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
3. With custome inits you set a default value and that can be comppuated like this one to turn inches to heights and vice versa, this makes the code dynamic

Another Example 


```

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

# Methods

```

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

Example with a mutating func


```


struct Post {
    var message: String
    var likes: Int
    var numberOfComments: Int

    mutating func like() {
        likes += 1
    }
}

// Create an instance of Post
var myPost = Post(message: "Hello, world!", likes: 10, numberOfComments: 5)

// Print likes before calling like()
print("Likes before: \(myPost.likes)")

// Call the like() method to increment likes
myPost.like()

// Print likes after calling like()
print("Likes after: \(myPost.likes)")


```



