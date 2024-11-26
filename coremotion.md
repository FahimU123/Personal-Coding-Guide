# Core Motion

```swift


import SwiftUI
import CoreMotion

// Class to manage accelerometer data
class MotionManager: ObservableObject {
    private let motionManager = CMMotionManager() // Core Motion manager to access accelerometer
    @Published var accelerometerData: String = "No Data" // Holds the accelerometer data to display
    
    // Initialize the motion manager and start accelerometer updates
    init() {
        startAccelerometerUpdates()
    }
    
    // Starts accelerometer updates and processes the data
    func startAccelerometerUpdates() {
        if motionManager.isAccelerometerAvailable { // Check if accelerometer is available on the device
            motionManager.accelerometerUpdateInterval = 0.1 // Set update frequency to 0.1 seconds
            
            // Start getting accelerometer data and handle it in the closure
            motionManager.startAccelerometerUpdates(to: OperationQueue.main) { [weak self] (data, error) in
                if let error = error { // If there's an error, show it
                    self?.accelerometerData = "Error: \(error.localizedDescription)"
                } else if let data = data { // If data is available, process it
                    let x = data.acceleration.x // Get x axis data
                    let y = data.acceleration.y // Get y axis data
                    let z = data.acceleration.z // Get z axis data
                    
                    // Update the accelerometer data to display
                    self?.accelerometerData = "x: \(x), y: \(y), z: \(z)"
                }
            }
        } else {
            accelerometerData = "Accelerometer not available." // If accelerometer isn't available, show a message
        }
    }
    
    // Stop accelerometer updates when MotionManager is deallocated
    deinit {
        motionManager.stopAccelerometerUpdates() // Stop updates to save resources and battery
    }
}

struct ContentView: View {
    @StateObject var motionManager = MotionManager() // Create an instance of MotionManager

    var body: some View {
        VStack {
            Text("Accelerometer Data:")
                .font(.title)
            Text(motionManager.accelerometerData) // Display the accelerometer data
                .padding()
                .font(.body)
        }
        .onAppear {
            motionManager.startAccelerometerUpdates() // Start accelerometer updates when the view appears
        }
    }
}

#Preview {
    ContentView() // Preview for SwiftUI ContentView
}


```

1. init(): Start the necessary updates or tasks when the object is created. For Core Motion, this typically means starting accelerometer updates, gyro data collection, etc.
2. deinit(): Stop the updates or tasks when the object is no longer needed. This helps save resources like memory, processing power, and battery.
3. Always when you import core motion you must create an instance of it
