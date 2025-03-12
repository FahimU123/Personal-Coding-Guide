# MenuBarExtra

```swift
import SwiftUI

@main
struct MenuBarExtraDemo: App {
    var body: some Scene {
        // Menu Bar Extra
        MenuBarExtra("Utility App", systemImage: "star.fill") {
            MenuBarContentView() // Separate view for the menu content
        }
    }
}
```

```swift
import SwiftUI

struct MenuBarContentView: View {
    var body: some View {
        Button("Show Settings") {
            print("Showing settings...")
        }

        Button("Quit") {
            NSApp.terminate(nil) // Quit the app
        }
    }
}

```
So this stuff will always be up as long as the app is in the background and will execute on the actio of the buttons
