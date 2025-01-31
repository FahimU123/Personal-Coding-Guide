# Dynamic Type

## Step 1: Get the size in your file with this line of code

```swift
struct ButtonArray: View {
    @Environment(\.dynamicTypeSize) var dynamicTypeSize
```

## Step 2:

```swift

let dynamicHStack = dynamicTypeSize <= .xLarge ? AnyLayout(HStackLayout()) : AnyLayout(VStackLayout())
        
let dynamicVStack = dynamicTypeSize <= .xLarge ? AnyLayout(VStackLayout()) : AnyLayout(HStackLayout())

```
1. Here we set a constant, then its basically saying, "hey, if its less then or equal to the large size then give me an HStck, otherwise give me a Vstack"
2. Vice versa with the second line of code

Note: 

```swift
 dynamicHStack{
            
    dynamicVStack{
        Text("Cut")
        Image(systemName: "person.crop.circle.badge.plus")
            .font(.headline)
            .dynamicTypeSize(...DynamicTypeSize.accessibility1)
            .frame(minWidth: 0, maxWidth:60, minHeight:20)
     }

```
- Here Im using the dynamic stacks, that `.dynamicTypeSize` modifier, I dont understand it too well BUT here are Joels words
- "this modifier actually limits dynamic type size. be careful when using it. this allows type to be resized up to accessibility 1 size"



# Bonus:

```swift
struct NiceParagraph: ViewModifier {
    func body(content: Content) -> some View {
        content
            .font(.body)
            .padding(.bottom, 7)
    }
}
```

Pretty self explantory, conform to this protocol and you can make your own modifiers

# 2nd Bonus:

```swift
extension View {
    func dynaButtonBG() -> some View {
        modifier(DynamicButtonBG())
    }
    
}
```

This extension allows for code compelteion for your custom modifier, which is cool

# ViewThatFits



1. ViewThatFits chooses a view that fits into the space - from top to bottom of the choices you list. 
2. When views are rendered, it chooses the best view that fits in every situation. In this case, as the text gets bigger, it goes down the list and picks the option that fits best.


``swift

ViewThatFits {
    Label("Welcome to AwesomeApp", systemImage: "bolt.shield")
        .font(.largeTitle)

    Label("Welcome", systemImage: "bolt.shield")
        .font(.largeTitle)

    Label("Welcome", systemImage: "bolt.shield")
}
```

