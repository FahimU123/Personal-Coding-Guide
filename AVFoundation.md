# AVFoundation

## Setting Up a Camera Feed

## 3 Big Things:
1. Start a camea session
2. Get camera input from the device
3. Display the feed

```swift
struct CameraView: UIViewRepresentable {
    func makeUIView(context: Context) -> UIView {
        let view = UIView()
```

1. Using this protocol because this bridges UIKit and SwiftUI and lets us use UIView
2. Samething with context

```swift
// Create a capture session
        let captureSession = AVCaptureSession()
```

```swift
 // Get the default camera
guard let camera = AVCaptureDevice.default(for: .video),
      let cameraInput = try? AVCaptureDeviceInput(device: camera) else {
    print("Unable to access camera")
    return view
}
```
1. First line gets the default camera for video
2. Second line gets the input which now can be used by the capture session
3. And a bunch of error handling

```swift

if captureSession.canAddInput(cameraInput) {
    captureSession.addInput(cameraInput)
}

```
Again, more error handling, would make the app crash if somehow we didnt have our camera input

```swift
let previewLayer = AVCaptureVideoPreviewLayer(session: captureSession)

```
1. The third big thing I was talking about
2. This actually diplays the live feed and you can add modifiers to this thing to make it sparkle
