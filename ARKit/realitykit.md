# ARkit/RealityKit


## Rules:

### **1. Start with `ContentView`**
- This is the main view that the user sees.
- Use a separate structure called `ARViewContainer` to handle all the AR tasks.

---

### **2. Use `UIViewRepresentable`**
- The `ARViewContainer` must conform to the `UIViewRepresentable` protocol.
- This lets you use UIKit’s `ARView` in SwiftUI.

---

### **3. Use `@Binding` for Communication**
- `@Binding` connects variables between the parent (`ContentView`) and the child (`ARViewContainer`).
- Changes in the AR view update the parent view, keeping them in sync.

---

### **4. `makeUIView` Sets Up the ARView**
- This function starts everything by creating and configuring the AR view.
- You can also customize its size.

---

### **5. Check Device Support**
- Use `ARBodyTrackingConfiguration.isSupported` to see if the device can handle body tracking.
- This avoids crashes on unsupported devices.

---

### **6. Configure the AR Session**
- Create the configuration type you want.
- This tells ARKit what type of tracking to perform.

---

### **7. Run the AR Session**
- Start the AR session with your chosen configuration.
- This activates the tracking.

---

### **8. Set the Delegate**
- Assign the `Coordinator` as the delegate for the AR session.
- The `Coordinator` acts as the helper or bridge that handles updates from the AR session and sends them to your app.

---

### **9. Add `updateUIView`**
- Use this function to handle updates to the ARView when the app state changes.

---

### **10. Create a Coordinator Class**
- The `Coordinator` class must conform to `NSObject` and `ARSessionDelegate`.
- These protocols are needed to handle AR session events, like body tracking updates.

---

### **11. Initialize the Coordinator**
- Since it’s a class, you need to initialize it.
- Pass in the `@Binding` variables so the Coordinator can update the UI in `ContentView`.

---

### **12. Process the AR Session**
- In the `session(_:didUpdate:)` method, loop through all the anchors updated by the AR session.

---

### **13. Filter for Body Anchors**
- Only process the anchors that are specifically body anchors (`ARBodyAnchor`).

---

### **14. Extract Positions**
- Get the positions of the body parts you want.
- Now you can find their 3D coordinates.
- AND NOW YOU CAN DO WHATEVER YOU WANT, EXTRACTING IS THE FOUNDTION, YOU HAVE THE DATA YOU NEED NOW IMPLEMENT THE LOGIC YOU NEED FOR YOUR PROJECT

---

### **15. Update the UI**
- Format the extracted positions (e.g., x, y, z coordinates) into a readable string.
- Use `DispatchQueue.main.async` to ensure the UI updates happen on the main thread.

---



```swift
import SwiftUI
import RealityKit
import ARKit

// SwiftUI View to display ARView
struct ContentView: View {
    var body: some View {
        ARViewContainer()
            .edgesIgnoringSafeArea(.all)


