# AVFoundation

## Setting Up a Camera Feed

```swift
let session = AVCaptureSession() // 1. Create a camera session
```
```swift
session.sessionPreset = .high // Set video quality to high
```
```swift
// 2. Select the front camera (or the back camera if you prefer)
        guard let device = AVCaptureDevice.default(.builtInWideAngleCamera, for: .video, position: .front),
              let input = try? AVCaptureDeviceInput(device: device) else {
            print("Error accessing camera")
            return view
        }

```
```swift
 session.addInput(input) // 3. Add the camera as an input to the session
```
```swift
 // 4. Create a preview layer to display the camera feed
        let previewLayer = AVCaptureVideoPreviewLayer(session: session)
        previewLayer.videoGravity = .resizeAspectFill // Make sure the video fits the screen
        previewLayer.frame = view.bounds // Match the layer size to the view
        view.layer.addSublayer(previewLayer)
```

```swift
 session.startRunning() // 5. Start the camera session
```

## How to use audio files in your app

```swift

var player: AVAudioPlayer? 

func playSound() {
    guard let path = Bundle.main.path(forResource: "beep", ofType:"mp3") else {
        return }
    let url = URL(fileURLWithPath: path)

    do {
        player = try AVAudioPlayer(contentsOf: url)
        player?.play()
        
    } catch let error {
        print(error.localizedDescription)
    }
}
```

1. Adjust extension and file name as necessary
