# ARKit

## Camera Setup

Step 1:

```swift
class CustomARView: ARView {
    required init(frame frameRect: CGRect) {
        super.init(frame: frameRect)
    }
    
    dynamic required init?(coder decoder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }
    
    // This is the init that we will actually use
    convenience init() {
        self.init(frame: UIScreen.main.bounds)
    }

```

1. class inherits from ARView which is from ARKit
2. First init sets up the paraamter of the view as a rectangle

Step 2:

```swift
import SwiftUI

struct CustomARViewRepresentable: UIViewRepresentable {
    func makeUIView(context: Context) -> CustomARView {
        return CustomARView()
    }
    
    func updateUIView(_ uiView: CustomARView, context: Context) { }
}
```

1. We use this protocol to integrate a UIView with SwiftUI
2. To conform to the protocol we need both of those funcs
3. This did used to retur a UIView but its faster if we return our CustomARView
