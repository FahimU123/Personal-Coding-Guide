# SceneKit

## How to create stuff with just code

Rules/Must Knows

1. A SCNNode is the building block, kind of like a container for all the visual stuff, similair to a model entity in relaity kit
2. A SCNGeometry  are the 3D shapes like planes, cubes, etc...
3. SCNMaterial is the color, texture just like relaitykit
4. You must understand the hierarchy, google a picture, basically image a family tree and the rootNode is the grandparent, eveyrthing moves relative to it, its the starting point, \
   hence you have to do the whole addChild thing for every SCNNode

```swift

 func setupHomeFlag() {

        let flagPlane = SCNPlane(width: 1.5, height: 0.75)  // step 1: setup the geometry

        flagPlane.firstMaterial?.diffuse.contents = UIImage(named: "flag.png") // step 2: setup materials
        flagPlane.firstMaterial?.isDoubleSided = true // put this if u wnat, self explantory, is optional
        
        let flagNode = SCNNode(geometry: flagPlane) // step 3: bring it all together, and craeet the node and attach to the geometry
        flagNode.position = SCNVector3(3, 0, 0) // optional
        rootNode.addChildNode(flagNode)
        
        let poleGeometry = SCNCylinder(radius: 0.05, height: 2.5)  //samething
        poleGeometry.firstMaterial?.diffuse.contents = UIColor.black
        let poleNode = SCNNode(geometry: poleGeometry)
        poleNode.position = SCNVector3(-0.8, -0.75, 0)

        flagNode.addChildNode(poleNode)
        
        
    }

