# Adapter

## "Allows obejcts with incompatible interfaces to collab" - Refactoring Guru
## Example: Your app always shows farenheight, you introduce a new weatherAPI which has everything in Celsisus so you use Adapter pattern for your app so you cna use this API and your app still gets Farenhigt

1. Implement your new library - this is called the adaptee
2. Define the target interface - Createing a protocol which inlcudes a method to convert the data into the necessary format
3. Create the adapter - A class which conforms to your target interface and has a properyy of that target interface type and use DI(dependecy inhection), and implement the method for the target interface 

# Proxy
## A placeholder obejct that can do things in place of the real object
## Example:

```swift
// Subject (protocol) - Have methods that do consuming tasks by your object
protocol Image {
    func display()
}

// Real Subject (concrete class) - Contains the bussiness logic for your actual obejct, conform to subject protocol
class RealImage: Image {
    private var filename: String
    init(filename: String) {
        self.filename = filename
        loadFromDisk()
    }
    private func loadFromDisk() {
        print("Loading image: \(filename)")
    }
    func display() {
        print("Displaying image: \(filename)")
    }
}

// Proxy (concrete class) - Conform to the subject protocol, have a properyy whuch expects the real subject and then initialize, then implement the protocol method
class ImageProxy: Image {
    private var realImage: RealImage?
    private var filename: String
    init(filename: String) {
        self.filename = filename
    }
    func display() {
        if realImage == nil {
            realImage = RealImage(filename: filename)
        }
        realImage?.display()
    }
}

// Client
let image: Image = ImageProxy(filename: "sample.jpg")
// The image is not loaded until the display method is called
image.display()

```
- Code by SwiftlyNomad
