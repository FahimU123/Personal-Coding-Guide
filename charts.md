# Charts

## Static Example

```swift
struct SalesData: Identifiable {
    let id = UUID()
    let day:  String   // x axix
    let sales: Double  // y axis
}
struct ContentView: View {
    let data: [SalesData] = [
        SalesData(day: "Mon", sales: 88),
        SalesData(day: "Tues", sales: 83)
    ]
    var body: some View {
        Chart(data) {item in
        BarMark(
            x: .value("Day", item.day),
            y: .value("Value", item.sales)
            )
            }
        .padding()
        .foregroundStyle(.orange)
        }
}

    
#Preview {
    ContentView()
}
```

#### 1: Create a struct and hold all the data your data set has in it and conform to identifiable
#### 2: Create some dummy data
#### 3: Gotta type Chart to start the process
#### 4: You can add a bunch of modfiers

## Dynamic Data Rules:

#### 1. Pretty much the same, craete a struc defining all properties fo your data
#### 2. Instead of creating dummy data create a var to store that data and conform it to your struct
#### 3. Now obsviously yur var which holds your data is empty SO you will populate it with a function and thats the big differnce
