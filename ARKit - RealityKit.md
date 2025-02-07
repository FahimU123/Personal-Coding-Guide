# ARKit/RealityKit

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

## Placing an Object

Step 1: Configuration

```swift

func configurationExamples() {
        // Tracks the device relative to it's environment
        let configuration = ARWorldTrackingConfiguration()
        session.run(configuration)
        
        // Not supported in all regions, tracks w.r.t. global coordinates
        let _ = ARGeoTrackingConfiguration()
        
        // Tracks faces in the scene
        let _ = ARFaceTrackingConfiguration()
        
        // Tracks bodies in the scene
        let _ = ARBodyTrackingConfiguration()
    }

```

1. Gotta figure what configuration your app needs
2. Then add the configuration to the session as shown above


Step 2: Anchors

```swift
 func anchorExamples() {
        // Attach anchors at specific coordinates in the iPhone-centered coordinate system
        let coordinateAnchor = AnchorEntity(world: .zero)
        
        // Attach anchors to detected planes (this works best on devices with a LIDAR sensor)
        let _ = AnchorEntity(plane: .horizontal)
        let _ = AnchorEntity(plane: .vertical)
        
        // Attach anchors to tracked body parts, such as the face
        let _ = AnchorEntity(.face)
        
        // Attach anchors to tracked images, such as markers or visual codes
        let _ = AnchorEntity(.image(group: "group", name: "name"))
        
        // Add an anchor to the scene
        scene.addAnchor(coordinateAnchor)
    }
```
1. This basically controls where the oject you will soon create will be placed

Step 3: Entities

```swift

func entityExamples() {
        // Load an entity from a usdz file
        let _ = try? Entity.load(named: "usdzFileName")
        
        // Load an entity from a reality file
        let _ = try? Entity.load(named: "realityFileName")
        
        // Generate an entity with code
        let box = MeshResource.generateBox(size: 1)
        let entity = ModelEntity(mesh: box)
        
        // Add entity to an anchor, so it's placed in the scene
        let anchor = AnchorEntity()
        anchor.addChild(entity)
    }

  func placeBlock(ofColor color: Color) {
        let block = MeshResource.generateBox(size: 1)
        let material = SimpleMaterial(color: UIColor(color), isMetallic: false)
        let entity = ModelEntity(mesh: block, materials: [material])
        
        let anchor = AnchorEntity(plane: .horizontal)
        anchor.addChild(entity)
        
        scene.addAnchor(anchor)
    }
}

```

1. These are different ways to add entities
2. Once you create or import your entity, you do the addChild line of code and add it to the scene as shown above, boom your done


## Components

```swift

// Define the custom component
struct AudioDataComponent: Component {
    var audioFileName: String
}

// Create your entity
let playButtonEntity = Entity()

// Attach the component to the entity
playButtonEntity.components.set(AudioDataComponent(audioFileName: "audio1.mp3"))

// Later, retrieve the component
if let audioComponent = playButtonEntity.components.get(AudioDataComponent.self) {
    let audioFileName = audioComponent.audioFileName
    print("Playing audio file: \(audioFileName)")
    // Play the audio file using the retrieved file name
}

```
1. Entites at the end of the day are limited, no way to do things like storing an audio file, soloution == Components protocol
2. By creating a custom component you can store this data and attach to the entity of your choice via `componenets.set`
3. Then you can use it as shown above
   

# Resources
1. BTW there are all sort of mesh resources and materials, just google them and the Apple doc has a lot of info. You can even have your own resources with `TextureResource`
2. Also to see how basic, built in gestures are done see [this](https://medium.com/@itsuki.enjoy/ios-swift-handle-3d-gestures-with-arkit-realitykit-3f7fd1609c54)
3. If you want to center text at the same positions as your shape whether its a cube or anything, see [this](https://stackoverflow.com/questions/67716279/how-to-make-text-to-have-the-same-position-and-orientation-as-box)
4. You can transfrom any entity using `Transform`, check the docs and its properties [here](https://developer.apple.com/documentation/realitykit/transform)
5. You can choose th eposition of an entity via `position`, check out [this](https://www.delasign.com/blog/how-to-set-the-position-scale-or-rotation-of-a-model-in-realitykit/)
6. Custom Gestures [here](https://www.createwithswift.com/adding-custom-gestures-to-an-ar-application-with-swiftui/)
7. Adding spatial audio [here](https://www.createwithswift.com/adding-spatial-audio-to-an-entity-with-realitykit/)


