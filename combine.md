# Combine

## Combine is basically a way to "watch" things and automatically react when they change.

## Rules: Need a Publisher, and a Subscriber

### Publisher listens for changes and a subscriber does something when that change happens

```swift


import HealthKit
import Combine

// Step 1: Define a Publisher
let healthStore = HKHealthStore()

let stepCountType = HKQuantityType.quantityType(forIdentifier: .stepCount)!
let stepCountPublisher = healthStore.publisher(for: stepCountType)  // This is a fictional example to illustrate the concept.

let stepsSubscriber = stepCountPublisher.sink { stepCount in
    print("Step count updated: \(stepCount)")
    // You can update your chart or UI here based on the new step count.
}

```



