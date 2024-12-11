# ARkit/RealityKit


## Rules:

You should create a separate struct to handle all AR-related functionality, typically named ARViewContainer.

Conform to UIViewRepresentable:
The struct must conform to UIViewRepresentable. This allows it to integrate ARKit with SwiftUI.

Implement makeUIView:
Create a makeUIView function that returns an ARView.

In this function, configure the AR session with the necessary settings (e.g., body tracking, face tracking, etc.).
After setting up the configuration, run it on the ARView and then return the ARView.
Add Entities:

Entities represent objects or parts of the environment that the camera will focus on. For example, in body tracking, entities could represent body parts like knees or hips.
Adding entities lets ARKit know what to track.

Implement updateUIView:

Include the updateUIView function to handle updates. This is commonly seen in most UIViewRepresentable examples.

Check for Device Support:

It's good practice to check if the current device supports the AR features you need (e.g., body tracking).
Track Entities:

Configure your session to track specific entities (e.g., body parts). Without explicitly enabling entity tracking, ARKit won't process them.

Detect Entities:

Create a function to detect and anchor the entities:

Use a body anchor to represent where the tracked entities are located in the 3D space.
Fetch body tracking data from the session to get precise positions of the body parts.

Add Models to Entities:

Once you have the positions of the body parts (e.g., knees, hips), you can create and attach 3D models to these parts.


```swift

import SwiftUI
import RealityKit
import ARKit

struct ARViewContainer: UIViewRepresentable {
    func makeUIView(context: Context) -> ARView {
        let arView = ARView(frame: .zero)
        
        // Check if body tracking is supported on this device
        guard ARBodyTrackingConfiguration.isSupported else {
            print("Body tracking is not supported on this device.")
            return arView
        }
        
        // Configure ARKit for body tracking
        let config = ARBodyTrackingConfiguration()
        arView.session.run(config)
        
        // Optionally, add entities to the AR view
        addBodyTrackingEntities(to: arView)
        
        return arView
    }
    
    func updateUIView(_ uiView: ARView, context: Context) {
        // Update logic for the AR view, if needed
        // For example, updating tracked body parts' positions
    }
    
    // Function to add body tracking entities (knees, hips)
    private func addBodyTrackingEntities(to arView: ARView) {
        let bodyAnchor = AnchorEntity(plane: .horizontal)
        
        // Fetch body tracking data
        guard let frame = arView.session.currentFrame,
              let body = frame.rawFeaturePoints?.arBody else { return }
        
        // Get the positions of the knees and hips
        if let leftKneeTransform = body.jointTransform(for: .leftKnee),
           let rightKneeTransform = body.jointTransform(for: .rightKnee) {
            
            // Create and position knee models
            let leftKneeModel = createKneeModel(at: leftKneeTransform.translation)
            let rightKneeModel = createKneeModel(at: rightKneeTransform.translation)
            
            // Add models to the body anchor
            bodyAnchor.addChild(leftKneeModel)
            bodyAnchor.addChild(rightKneeModel)
        }
        
        arView.scene.addAnchor(bodyAnchor)
    }
    
    // Function to create a knee model
    private func createKneeModel(at position: SIMD3<Float>) -> ModelEntity {
        let model = ModelEntity(mesh: .generateSphere(radius: 0.05), materials: [SimpleMaterial(color: .red, isMetallic: false)])
        model.position = position
        return model
    }
}
