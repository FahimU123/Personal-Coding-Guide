# onHover

```swift
struct ContentView: View {
    @State private var overText = false

    var body: some View {
        Text("Hello, World!")
            .foregroundStyle(overText ? .green : .red)
            .onHover { over in
                overText = over
            }
    }
}
```

1. So here if `overText` is true then when you hover over Hello World it will be green otherwise red 
