# Bridging SwifUI & UIKit

```swift
import UIKit

class CustomUILabel {
    static func createLabel(text: String) -> UILabel {
        let label = UILabel()
        label.text = text
        label.textAlignment = .center
        label.textColor = .white
        label.backgroundColor = .blue
        return label
    }
}
```

1. Here you have a nice label but it was made in UIKit and you want to use it in SwiftUI


## Rules

```swift

import SwiftUI

// Step 1: Conform to UIViewRepresentable which kinda bridges SwiftUI and UIkit
struct MyUILabel: UIViewRepresentable {
    var text: String

 typealias UIViewControllerType = UILabel // <- Choose the correct controller (IDK if this is necessary since Swift is type safe but a bunch of articles have it) - it basically tells it the type, simply put

    // Step 1: Create this func, creating the view
    func makeUIView(context: Context) -> UILabel {
        // Use the CustomUILabel class to create and configure the UILabel
        return CustomUILabel.createLabel(text: text)
    }

    // Step 3: Now make this func, updating the view
    func updateUIView(_ uiView: UILabel, context: Context) {
        uiView.text = text
    }
}

```

## Implemnetaion 

```swift
struct ContentView: View {
    var body: some View {
        VStack {
            Text("Hello from SwiftUI!")
                .font(.title)
                .padding()

            // Use the UIKit UILabel in SwiftUI
            MyUILabel(text: "Hello from UIKit!")
                .frame(width: 200, height: 50)
                .padding()
        }
    }
}
```

1. And now you can use `MyUILabel` in SwiftUI

