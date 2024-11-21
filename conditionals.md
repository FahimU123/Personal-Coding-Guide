# Conditionals

### Else if

```swift
let anotherVideoLength = 75000

if anotherVideoLength < 5 {
    "If I blinked, I'd miss it."
} else if anotherVideoLength > 50000 {
    "This is too long for anyone."
} else if anotherVideoLength > 500 {
    "Don't worry, I know a good editor."
} else {
    "That was lovely."
}

```
1. You can have as many else if you want in between the if and the final else(not efficient)


# Nesting Conditianals


```swift

let chanceOfRain = 0.5

let bulkiestItemWeight = 60

if gearWeight < totalCarryingCapacity {
    if bulkiestItemWeight < 80 {
        "Rock on."
    } else if chanceOfRain >= 0.1 {
        "Everyone quits! Looks like you've got a solo show."
    }
} else {
    "Everyone quits! Looks like you've got a solo show."
}

```


1. The first if statement will return a boolean and if true it will then move to the 2nd if statement. If false it will just jump down to the else statement.
2. If the second if statemnt happnes to be true it will print "Rock on"
3. If only the first if statement was true but not the second one it will print "Everyone quits! Looks like you've got a solo show."

# Functions && Conditionals

```swift

func bandCanCarryGear(bandMemberCount: Int, gearWeight: Int, bulkiestItemWeight: Int, chanceOfRain: Double) -> Bool {
    let maximumTripCount = 2
    let weightPerPerson = 50
    let totalCarryingCapacity = bandMemberCount * weightPerPerson * maximumTripCount
    
    return gearWeight < totalCarryingCapacity && (chanceOfRain < 0.1 || bulkiestItemWeight < 80)
}

print((bandCanCarryGear(bandMemberCount: 2, gearWeight: 100, bulkiestItemWeight: 25, chanceOfRain: 0)))

if bandCanCarryGear(bandMemberCount: 5, gearWeight: 650, bulkiestItemWeight: 60, chanceOfRain: 0.05) {
    "Rock on."
} else {
    "Everyone quits! Looks like you've got a solo show."
}


```

1. When you use a function that has paramaters in an if statement you must still pass paramaters in the if statement.


# Modulo? Remainder Operator


```swift


let bandMemberCount = 6

let candyCount = 79

if candyCount % bandMemberCount == 0 {
    "Rock on."
} else {
    "Everyone quits! This is unacceptable!"
}

```

1. The % means it will perform the devison and give you the remainder
2. In this case the remainder is one
3. Hence, the else statemnet prints

# Switch Statements

```swift

var birthMonthNumber = 2

switch birthMonthNumber {
case 1:
    print("January")
case 2:
    print("February")
case 3:
    print("March")
case 4:
    print("April")
default:
    print("you should double check your birth certificate")
}

```

1. Must have a default scenario for a catch all statements
