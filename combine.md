# Combine

## Combine is basically a way to "watch" things and automatically react when they change.

## Rules: Need a Publisher, and a Subscriber

### Publisher listens for changes and a subscriber does something when that change happens

```swift


class TextViewModel: ObservableObject {
    @Published var textInput: String = ""  // Publisher: This is the source of changes.
    @Published var uppercaseText: String = ""  // Publisher: This holds the updated value.

    private var cancellables = Set<AnyCancellable>()  // Dont;t need it here but will show why its important in other cases below

    init() {
            .map { $0.uppercased() }  // Operator: Transforms the text to uppercase.
            .assign(to: &$uppercaseText)  // Subscriber: Automatically updates `uppercaseText` when `textInput` changes.
    }
}

struct ContentView: View {
    @StateObject private var viewModel = TextViewModel() 

    var body: some View {
        VStack {
            // The TextField binds to the `textInput` property of the view model.
            // This acts as a subscriber to the publisher `$textInput` via the `@StateObject`.
            TextField("Type something...", text: $viewModel.textInput)
                .padding()
                .textFieldStyle(RoundedBorderTextFieldStyle())

            // This Text view will display the `uppercaseText` value that is automatically updated by Combine.
            Text("Uppercase: \(viewModel.uppercaseText)")
                .font(.headline)
        }
        .padding()
    }
}


```

1. When to Use @Published vs. @State:
@Published:	When sharing data between views or managing with a class. Inside an ObservableObject class
@State: For local, simple state tied to one view. Inside a SwiftUI View struct

### Cancellable

A **cancellable** is like a **"stop sign"** for a subscription in Combine. When you subscribe to a **publisher** (like `$textInput`), it sends updates. A **cancellable** helps you stop or **cancel** that subscription when you don’t need it anymore.

---

### Why Do You Need It?

If you don’t **cancel** the subscription, Combine might keep sending updates even when you don’t need them anymore, which can waste resources or cause memory leaks.

---

### How It Works:

1. You **subscribe** to a publisher (like `$textInput`).
2. The publisher sends updates (like when text changes).
3. The **cancellable** keeps track of this subscription.
4. When you no longer need it, you can **cancel** it (using the cancellable) to stop receiving updates.

---

### In Simple Code:

```swift
let subscription = publisher
    .sink { value in
        print(value)
    }

// You can cancel it like this:
subscription.cancel()  // No more updates!
```

**Cancellable** helps manage when and how long you want to "listen" to a publisher for updates.

