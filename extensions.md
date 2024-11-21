# Extensions

Extensions are used to add funtionaly to existing datay types, either custom or built in data types

```swift


class Temperature {
  var celsius: Double = 0

  func setTemperature(celsius: Double) {
    self.celsius = celsius
    print("Celsius:", celsius)
  }
}

extension Temperature {


  func convert() {
    var fahrenheit = (celsius * 1.8) + 32
    print("Fahrenheit:", fahrenheit)
  }
}

let temp1 = Temperature()
temp1.setTemperature(celsius: 16)

temp1.convert()

```

1. Here we have a temperature class which is a data type so we can create an exttension for it and we do in this example
2. In the extension the convert method is added
3. Now after the constant is set we can access the method in the class ASWELL as the extension

# Computed Properties and Extensions

```swift

class Circle {
  var radius: Double = 0
}

extension Circle {
  var area: Double {
    return 3.14 * radius * radius
  }
}

let circle1 = Circle()
circle1.radius = 5
print("Area:", circle1.area)

```

1. Since Circle is a custom data type we can craete a extension for it
2. Notice the var is a Double, now if this was not a cumputed property and we were just storing the area as a Double it would throw and error but since its computed its okay.

# Protocol Extension

```swift

// protocol definition
protocol Brake {
  func applyBrake()
}

// extend protocol
extension Brake {
  func applyBrake() {
    print("Brake Applied")
  }
}

// define class that conforms Brake
class Car: Brake {
  var speed: Int = 0
}

let car1 = Car()
car1.speed = 61
print("Speed:", car1.speed)

// access extended protocol
car1.applyBrake()

```
