# Enums

# Basic Syntax 

```
enum LunchChoice {
    case pasta, burger, soup
}
 
let choice = LunchChoice.burger

var choice: LunchChoice

// If Swift already knows what type to expect, you can skip the enum name. Since you’ve already specified the type of `choice`, you can leave out the enum name when assigning a value:

choice = .burger

```

# Enums and Functions

```
enum LunchChoice {
    case pasta, burger, soup
}

func cookLunch(_ choice: LunchChoice) -> String {
    
    if choice == .pasta {
        return "🍝"
    } else if choice == .burger {
        return "🍔"
    } else {
        return "🍲"
    }
}

cookLunch(.burger)

```

1. The enum becomes a data type
2. Now inside the function if you use "choice" you can refer to any of the cases in enums

# Enums and Switches

```

enum Quality {
    case bad, poor, acceptable, good, great
}

let quality = Quality.bad

switch quality {
case .bad:
    print("That really won't do")
case .poor:
    print("That's not good enough")
default:
    print("OK, I'll take it")
}

```

1. When you use a switch your turning something on hence why the keyword "choice" is needed
2. Swicth allows for things to happen in certain cases
3. Notice the default case

# Enum Methods and Properties

```

enum LunchChoice {
    case pasta, burger, soup
    
    var emoji: String {
        switch self {
        case .pasta:
            return "🍝"
        case .burger:
            return "🍔"
        case .soup:
            return "🍲"
        }
    }
}
let lunch = LunchChoice.pasta
lunch.emoji

```

1. Since the computed property is in the enum itself, when you use switch you must also say self


# Great Example 

```

enum ClassTripDestination {
    case beach, chocolateFactory
}

let tripDestinationVotes: [ClassTripDestination] = [.beach, .chocolateFactory, .beach, .beach, .chocolateFactory, .chocolateFactory, .chocolateFactory, .beach, .beach, .beach, .chocolateFactory, .beach, .beach] 

var beach = 0
var choclateFactory = 0


for tripDestinationVote in tripDestinationVotes {
    if tripDestinationVote == .beach {
        beach += 1
    }
    else {
        choclateFactory += 1
    }
}

print(beach)
print(choclateFactory)

```
# Great Example With Switch Self and Static

```
struct swimmingWorkout {
    var distance: Double
    var time: Double
    var stroke: stroke
    static var freeStyleWorkputs: [swimmingWorkout] = []
    static var butterflyWorkouts: [swimmingWorkout] = []
    static var backStrokeWorkouts: [swimmingWorkout] = []
    static var breastStrokeWorkouts: [swimmingWorkout] = []
    
    enum stroke {
        case freestyle, butterfly, backstroke
    }
    
    func save() {
        switch self.stroke {
        case .backstroke:
            swimmingWorkout.backStrokeWorkouts.append(self)
        case .butterfly:
            swimmingWorkout.butterflyWorkouts.append(self)
        case .freestyle:
            swimmingWorkout.freeStyleWorkputs.append(self)
        }
    }
    
  
}
```
```

var workoutOne = swimmingWorkout(distance: 12, time: 2, stroke: swimmingWorkout.stroke.backstroke)

var workoutOTwo = swimmingWorkout(distance: 120, time: 20, stroke: swimmingWorkout.stroke.butterfly)

workoutOne.save()

workoutOTwo.save()

```

1. self refers to properties, Self refers to types like structs or enums
