# Windows Management

```swift
import SwiftUI

@main
struct MultiWindowDemo: App {
    var body: some Scene {
        // Main Window
        WindowGroup("Main Window", id: "main") {
            ContentView()
        }

        // Settings Window
        WindowGroup("Settings", id: "settings") {
            SettingsView()
        }
    }
}

```

1. In the @main file if you want multiple windows then give each window a name and id


```swift
struct ContentView: View {
    @Environment(\.openWindow) private var openWindow

    var body: some View {
        VStack {
            Text("Main Window")
                .font(.largeTitle)
            Button("Open Settings") {
                openWindow(id: "settings") // Open the Settings window
            }
        }
        .padding()
    }
}

```

1. Use @Envirement to open other windows
2. Then use the openWindow var to open other windows via the id you set
