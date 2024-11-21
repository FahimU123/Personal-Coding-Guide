# Generics

## Generics and Functions

```swift

func displayElements<T>(elements: [T]) {
    for element in elements {
        print(element)
    }
}

displayElements(elements: [2, "Test", true])

```

1. Generics allow for you to create a var and it can accept any data types, even custom ones
2. The part inside <> is called a generic paramater and after you put it in the <>, it has become a data type you can conform to in the functions paramaters
3. Now this func can take any data type and orint them

## Operators and Generics

```swift

func count<Number: Numeric>(numbers: [Number]) {
    let total = numbers.reduce(0, +)
    print("Total is \(total)")
}

count(numbers: [2, 3.5])

```

1. Here the Number generic parameter conforms to Numeric, meaning it can only take numeric numbers which allows for a user to enter CGFloats, Doubles, and even Ints
2. It must conform to Numeric here because it is doing a mathematical function and that means we have to only deal with numerical values


## Generics and Classes


```swift

class Information<T> {

  var data: T

  init (data: T) {
    self.data = data
  }


  func getData() -> T {
    return self.data
  }
}

var intObj = Information<Int>(data: 6)
print("Generic Class returns:", intObj.getData())

var strObj = Information(data: "Swift")
print("Generic Class returns:", strObj.getData())

strObj = Information(data: "Python")

```

1. Since as soon as the class was made you said it will all conform to the 'T' data type, now all properties and methods in that class must use 'T'
2. Once you make an instance of this class they can take any data type, but after that instance is locked in on a data type its locked in
3. See how when I changed strtOBJ value, it was changed to a string, that works, but if it was changed to say 8, it would throw an error
