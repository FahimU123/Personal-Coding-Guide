# SpriteKit - Collision

To enable collsion and its detection you must know THREE things

1. categoryBitMask - every node that is enabled for collision must have this, it's like the ID
2. collisionBitMask - this is set for the categories of objects that this node will physically be stopped by and push back against
3. contactTestBitMask - this alerts the didBegin function so not absolutely required if you don't have that

Refer to https://stackoverflow.com/questions/26702944/swift-spritekit-multiple-collision-detection/26723392#26723392 for best practices 
And this https://github.com/IlijaMihajlovic/Collision-Detection-in-SpriteKit/blob/master/Detect%20Contact%20in%20SpriteKit/GameScene.swift
