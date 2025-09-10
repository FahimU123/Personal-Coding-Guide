# State

## Good for managing state, especially if you have an increasing number of states 
## Example: 

Note: Use these naming conventions

```swift
// Step 1: State (protocol) - Have a method for all the different states of your object
protocol DocumentState {
    func edit()
    func review()
    func publish()
}

// Step 2: Concrete States - Create a class for every state and conform to your state protocol, and implement the methods for the protocol
class EditingState: DocumentState {
    func edit() {
        print("Already in editing state.")
    }
    func review() {
        print("Switching to review state.")
    }
    func publish() {
        print("Switching to published state.")
    }
}

class ReviewState: DocumentState {
    func edit() {
        print("Switching to editing state.")
    }
    func review() {
        print("Already in review state.")
    }
    func publish() {
        print("Switching to published state.")
    }
}

class PublishedState: DocumentState {
    func edit() {
        print("Document is in a read-only state.")
    }
    func review() {
        print("Switching to review state.")
    }
    func publish() {
        print("Already in published state.")
    }
}

// Step 3: Context - This is the class for the object that has all the states. It executes the proper method based on the current state,
class Document {

    // You must have it expect a state and set its default state
    private var state: DocumentState
    init() {
        self.state = EditingState()
    }

    // You must have a setState method that takes a parameter for state. Soemtimes called change state
    func setState(state: DocumentState) {
        self.state = state
    }

    // You must include all the methods so it can execute. Does not have to be the same name, but is best parc
    func edit() {
        state.edit()
    }
    func review() {
        state.review()
    }
    func publish() {
        state.publish()
    }
}

// Client
let document = Document()
document.edit()
document.review()
document.publish()
document.edit()
document.publish()
```
- Code from Swiftly Nomad





