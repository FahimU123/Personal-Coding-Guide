# CoreML-Vision

After setting up a cqpture session, refer to AVFoundation.md you can start here

1. Make sure to capture outputData and conform to AVCaptureVideoDataOutputSampleBufferDelegate in your ViewController

```swift
class ViewController: UIViewController,AVCaptureVideoDataOutputSampleBufferDelegate
let outputData = AVCaptureVideoDataOutput()
        outputData.setSampleBufferDelegate(self, queue: DispatchQueue(label: "videoQueue"))
        capture.addOutput(outputData)
        
```

```swift
// Step 2: Dot his func, thsi is how you conform to thats uper long protocol
 func captureOutput(_ output: AVCaptureOutput, didOutput sampleBuffer: CMSampleBuffer, from connection: AVCaptureConnection) {
        // Step 3: Gotta do this to extract the pixel data and take it from CVPixelBuffer to CMSampleBuffer(a formal these frameowrks understand)
        guard let pixelBuffer: CVPixelBuffer = CMSampleBufferGetImageBuffer(sampleBuffer) else{return}
        
        //   Step 4: Here you can add the most suitable model for you that you find on Apple site or put your own model in
        guard let model = try? VNCoreMLModel(for: Resnet50().model)else{return}

          // Step 5: Do this, everyone gotta do this
        let request = VNCoreMLRequest(model: model) { (finishRequest, error )in


             // Step 6: Gotta do this just make sure to properly choose what type you need, `VNClassificationObservation` - talking about this part
            guard let results = finishRequest.results as?[VNClassificationObservation] else{return}
            guard let observassion = results.first else{return}
            
           
            
        }
        try? VNImageRequestHandler(cvPixelBuffer: pixelBuffer, options: [:]).perform([request])
    }
    
    
    
```
