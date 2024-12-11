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

---

### **15. Update the UI**
- Format the extracted positions (e.g., x, y, z coordinates) into a readable string.
- Use `DispatchQueue.main.async` to ensure the UI updates happen on the main thread.

---



```swift
import SwiftUI
import RealityKit
import ARKit

struct ContentView: View {
    @State private var hipPosition: String = "Unknown"
    @State private var hipAngles: String = "Unknown"

    var body: some View {
        ZStack {
            ARViewContainer(hipPosition: $hipPosition, hipAngles: $hipAngles)
                .edgesIgnoringSafeArea(.all)

            // Display tracked hip position and angles
            VStack {
                VStack(alignment: .leading, spacing: 8) {
                    Text("Hip Position:")
                        .font(.headline)
                    Text(hipPosition)
                        .font(.body)
                        .foregroundColor(.white)
                        .padding(5)
                        .background(Color.black.opacity(0.6))
                        .cornerRadius(10)

                    Text("Hip Angles:")
                        .font(.headline)
                    Text(hipAngles)
                        .font(.body)
                        .foregroundColor(.white)
                        .padding(5)
                        .background(Color.black.opacity(0.6))
                        .cornerRadius(10)
                }
                .padding()
                Spacer()
            }
        }
    }
}

struct ARViewContainer: UIViewRepresentable {
    @Binding var hipPosition: String
    @Binding var hipAngles: String

    func makeUIView(context: Context) -> ARView {
        let arView = ARView(frame: .zero)

        guard ARBodyTrackingConfiguration.isSupported else {
            print("Body tracking is not supported on this device.")
            return arView
        }

        let config = ARBodyTrackingConfiguration()
        arView.session.run(config)
        arView.session.delegate = context.coordinator

        return arView
    }

    func updateUIView(_ uiView: ARView, context: Context) {}

    func makeCoordinator() -> Coordinator {
        Coordinator(hipPosition: $hipPosition, hipAngles: $hipAngles)
    }

    class Coordinator: NSObject, ARSessionDelegate {
        @Binding var hipPosition: String
        @Binding var hipAngles: String

        init(hipPosition: Binding<String>, hipAngles: Binding<String>) {
            _hipPosition = hipPosition
            _hipAngles = hipAngles
        }

        func session(_ session: ARSession, didUpdate anchors: [ARAnchor]) {
            for anchor in anchors {
                if let bodyAnchor = anchor as? ARBodyAnchor {
                    // Extract hip position
                    if let hipTransform = bodyAnchor.skeleton.modelTransform(for: .init(rawValue: "root")) {
                        let hipPosition = hipTransform.columns.3
                        DispatchQueue.main.async {
                            self.hipPosition = String(format: "x: %.2f, y: %.2f, z: %.2f", hipPosition.x, hipPosition.y, hipPosition.z)
                        }

                        // Calculate angles (dummy example for now)
                        let angleX = atan2(hipTransform.columns.1.z, hipTransform.columns.1.y) * (180 / .pi)
                        DispatchQueue.main.async {
                            self.hipAngles = String(format: "Angle X: %.2f°", angleX)
                        }

                        // Add visual representation
                        DispatchQueue.main.async {
                            self.addVisualRepresentation(for: session, at: [hipPosition.x, hipPosition.y, hipPosition.z])
                        }
                    }
                }
            }
        }

        func addVisualRepresentation(for session: ARSession, at position: SIMD3<Float>) {
            // Access ARView directly
            guard let arView = session.delegate as? ARView else { return }

            // Create a sphere for the hip joint
            let sphere = ModelEntity(mesh: .generateSphere(radius: 0.05), materials: [SimpleMaterial(color: .red, isMetallic: false)])
            sphere.position = position

            // Create an anchor and attach the sphere
            let anchor = AnchorEntity(world: position)
            anchor.addChild(sphere)
            arView.scene.addAnchor(anchor)
        }
    }
}
