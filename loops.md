# Loops

## For in Loops

```swift
let friends = ["Name", "Name2", "Name3", "Name4", "Name5"]

for friend in friends {
    let sparklyFriend = "✨\(friend)✨"
    print("Hey, \(sparklyFriend), please come to my party on Friday!")
}
print("Done, all friends have been invited.")

```

1. Naming is huge. Keep the "friends" part plural and the spot before singular.
2. The friend part does NOT have to be declared anywhere else. Its in the scope of that "for in" loop.
3. This code goes through every name and says Hey and chooses every name and says please come to the party to them.

### Another Example

```swift

for bottlesDrank in 0..<100 {
    print("\(bottlesDrank) bottles of beer have been drank,")
}
print("All of the beer is gone!")

```

1. Again "bottlesDrank" exists in that for loop and does not need to be declared anywhere else.
2. A closed range, from 0 all the way up-to-and-including 10.
let closedRange = 0...10
3. An open range, from 4 up to 13, but NOT including 13. (12 is the max)
let openRange = 4..<13
4. This code will say 0,1,2 and so on bottles of beer have been drank(Astagfirullah) and then print ALL of the beer is gone(2xAstagfirullah)

### Another Example with Arrays, Appending, and removeAll

```swift
var songTitles: [String] = ["22"]
songTitles.append("Rap God")
songTitles.append("IDK")

var nathansSong = ["Alive", "I'm Yours", "I'm Yourself"]

songTitles += nathansSong

for song in songTitles {
    print("Its time for \(song)")
}

songTitles.removeAll()
print(songTitles)


```

1. Using append I can add things to my array
2. I can add a whole variable to my array aswell as long its the same type

### Another Example with +=, varsity, and conditionals

```swift


let shouldMascotChangeVotes: [Bool] = [false, false, false, true, false, true, true, true, false, true, true, true, true, false, true, true, false, true, true, true, false, true, true, true, true, true, true, true, false, true, false, true, false, true, true]

var yes = 0
var no = 0

for vote in shouldMascotChangeVotes {
    if vote == true  {
        yes += 1
    } else {
        no += 1
    }
}
    print(yes)
    print(no)

```

1. Again vote exixts in the for loop and does not need to be declared elsewhere
2. The += adds 1 to the var and likewise for no

## While Loops

```swift
var randomNumber = Int.random(in: 0...10)

//The loop will run as long as random number doesn't equal 6.
while randomNumber != 6 {
    randomNumber = Int.random(in: 0...10)
    print("Right now we're at \(randomNumber)")

```

1. As long as the number is not 6 this code will run

### More complex example

```swift

var alicesMessages = ["Mouse: Hello!", "Alice: Hello, mouse!", "Mouse: How are you?", "Alice: Fine, thanks!", "Mouse: Oh look, there's a cat!", "Cat: Meow!", "Alice: Meeeeeow..."]

for i in 0...alicesMessages.count - 1 {
    if alicesMessages[i].contains("Cat") {
        print("Cat has a line at \(i)")
    }
}

var catArrived = false
var i = 0

while !catArrived {
    if alicesMessages[i].contains("Cat") {
        print("Cat has a line at \(i)")
        catArrived = true
    } else {
        i += 1
    }
}

```



1. A bool is necessary
2. When that bool turn true write the action code
3. Toggle the bool to true when it it meets the condition(s) for it to stop
4. Otherwise have an else statemnt that keeps the loop going

## Function and Loops

```swift

let shouldMascotChangeVotes: [Bool] = [false, false, false, true, false, true, true, true, false, true, true, true, true, false, true, true, false, true, true, true, false, true, true, true, true, true, true, true, false, true, false, true, false, true, true]

func printResults(theString: String, withVotes: [Bool]) {
    var yesCount: Int = 0
    var noCount: Int = 0
    
    for vote in withVotes {
        if vote {
            yesCount += 1
        } else {
            noCount += 1
        }
    }
    print("\(theString) , \(yesCount), yes, \(noCount) , no")
    

}
printResults(theString: "so we chnage the mascot", withVotes: shouldMascotChangeVotes)

```

1. In the function in the () you can pass in different values and data types.
2. Now this code can run for any sets of data in arrays to calculate votes

### Aother way to do the same code:

```swift

var pollOptionYes = 0
var pollOptionNo = 0

for vote in shouldHaveMorePollOptionsVotes {
    if vote == true  {
        pollOptionYes += 1
    }
    else {
        pollOptionNo += 1
    }
}
print("Poll Option Votes: \(pollOptionYes) Yes, \(pollOptionNo) No")

```

## More Functions and Loops

```swift
let hoursSlept = [8, 8, 8, 8 ,9 , 10 ,9, 7, 9, 9, 9, 7, 8, 8, 9, 9, 8 , 10, 10, 9, 9, 9, 9, 9, 9]

func numbers(hours: [Int]) {
    for hour in hours {
        if hour > 8 {
            print("dq")
        }else {
            print("fewf")
        }
    }
}
numbers(hours: hoursSlept)

```

1. In the () theres a var which you can do with any funcs
2. In order to run through every line of code and get a print result you must refer to the var in the ()
3. Again the first var in a for loop can be anything but for namessake make it the singualr version of the 2nd one


### Another example with the i 
```swift
let colors = ["Red", "Orange", "Yellow", "Green", "Blue", "Indigo", "Violet"]

for i in 0 ... colors.count - 1 {
    print("\(i): \(colors[i])")

```

1. The colors.count - 1 is for making sure it doesnt go above the amount since theres 7 colors and we minus one because the positions start at 0
2. The i is for the current position and the \(colors[i]) will print out the color in that position

### Simialiar Examples

```swift

var fruits = ["apples", "oranges", "peaches"]

for i in 0 ... fruits.count - 1 {
    if fruits[i] == "apples"{
        print("\(i): \(fruits[i])")
    }
}

```


### ForEach

```swift
struct ContentView: View {
    let items = ["Apple", "Banana", "Cherry"]

    var body: some View {
        VStack {
            ForEach(items, id: \.self) { item in
                Text(item)
            }
        }
    }
}
```

1. For some reason you can youse a regular for loop in a SwiftUI view so you do this

