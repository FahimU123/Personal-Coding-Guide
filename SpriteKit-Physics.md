# SpriteKit - Physics

Physics refers to how these nodes/objects would move as if they were in the real world

- Just give your node physics body
- Then you can adjust the physics properties by changing the methods to your liking

So, for example, if you wanted your sprite to fall but not just ina straight line from the sky, then tweak the gravity, which is a physics method you can adjust or tweak the angular velocity or whatever.

```swift
func spawnCell() {
    let cell = SKSpriteNode(imageNamed: "cancerCell")
    // ... position cell at the top...

    // Give it a physics body
    cell.physicsBody = SKPhysicsBody(circleOfRadius: cell.size.width / 2)
    cell.physicsBody?.isDynamic = true
    
    // Set a random initial horizontal speed (-50 to +50)
    let randomPush = CGFloat.random(in: -50...50) 

    // Apply the initial velocity (starts moving horizontally)
    cell.physicsBody?.velocity = CGVector(dx: randomPush, dy: 0) 
    
    addChild(cell)
}
