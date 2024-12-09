# ARkit/RealityKit


## Rules:
1. You want to create a seperate struct to handle all your AR stuff, usually called ARViewContainer
2. That struct should conform UIViewRepresenatble
3. Should have a func called makeUIView which returns an ARView
4. In that func you should configure to the necessary configuration you need and run the config, then you can return an ARView
5. Now you can add an entity which is basically what the camera should focus on, so if it was a body config then you can make say knees and hips the entities
6. Also have an updateUIView func because I guess thats important to handle uodates and I see it in every example
7. Checking if its supported is good practice
8. Config isnt enough you must also say you want to add entities which is basically things you want to focus on in the camera
9. Now once youve said you wnat to track enttites then you can create a fucn to detect them
10. In that func you must create a body anchor which serves as where your entities would go
11. Also fetch the body tracking data
12. Now that you have the data you can grab the position of the specific body parts you want
13. Then you can create models that go on those body parts


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
