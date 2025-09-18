the raw# OptionSet

This is a protocol used to describe options. Think of using it for a situation where on a form you would check multiple boxes, where like when an enum, you can check one box

1. First, you describe all the options and give them a raw binary value
```swift
   struct ShippingOptions: OptionSet {
   // If you had multiple options, the raw value would combine the binary values of all options
    let rawValue: Int

    // these are the bitwise left shift operator, which auto-increments the binary value by powers of 2
    static let nextDay    = ShippingOptions(rawValue: 1 << 0)
    static let secondDay  = ShippingOptions(rawValue: 1 << 1)
    static let priority   = ShippingOptions(rawValue: 1 << 2)
    static let standard   = ShippingOptions(rawValue: 1 << 3)


    static let express: ShippingOptions = [.nextDay, .secondDay]
    static let all: ShippingOptions = [.express, .priority, .standard]
}
```
2. You combine all these options in an array to your liking
```swift
let singleOption: ShippingOptions = .priority
let multipleOptions: ShippingOptions = [.nextDay, .secondDay, .priority]
let noOptions: ShippingOptions = []

```
3. OptionSet conforms to SetAlgebra, so it gets access to all the methods of that protocol, so you can use them on the different options
 ```swift
   let purchasePrice = 87.55


var freeOptions: ShippingOptions = []
if purchasePrice > 50 {
    freeOptions.insert(.priority)
}


if freeOptions.contains(.priority) {
    print("You've earned free priority shipping!")
} else {
    print("Add more to your cart for free priority shipping!")
}
// Prints "You've earned free priority shipping!"
```
- ALL EXAMPLE CODE FROM APPLE DOCS - REFER TO THEM
