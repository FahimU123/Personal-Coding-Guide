# MacOS Commands

```swift
import SwiftUI

@main
struct MenuBarCommandsDemo: App {
    var body: some Scene {
        WindowGroup {
            ContentView()
        }
        .commands {
            MyCustomCommands()
        }
    }
}
```

1. Create a separate structure and have your commands there but in your App struct just have this



```swift
import SwiftUI

struct MyCustomCommands: Commands {
    var body: some Commands {
        CommandMenu("Custom Menu") {
            Button("Refresh Content") {
                print("Refreshing content...")
            }
            .keyboardShortcut("R", modifiers: [.command])
    }
}

```
1. Conform to 'Commands`
2. That first keyboard shortcut is basically command + R
3. You can add multiple buttons within this CoomandMenu aswell
4. These are the menu items on the left side of the screen when you opne a macOS app







