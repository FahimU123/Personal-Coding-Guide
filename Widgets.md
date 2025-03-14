# Widgets

## Must Haves:

### A struct for the data you wil display on your widget
### A widget vies where you use SwiftUI to make your widget
### A provider struct, this ones the big one
1. Of course import WidgetKit
2. Your structure should conform to `TimelineProvider`

### A structure conforming to `TimelineEntry`
### And your in @main file you must conform to `Widget` 

# Step 1: 

```swift
struct Tips {
    var tipsList: [String] = [
        "Stay Hydrated: Drinking an adequate amount of water daily is crucial for maintaining overall health and well-being. Aim for at least 8 glasses (64 ounces) of water per day, but individual needs may vary.",
        "Listen to Your Body: Pay attention to signals like fatigue, mood changes, or changes in appetite. Your body often communicates its needs, and listening to it can help you maintain good health.",
        "Prioritize Sleep: Quality sleep is essential for physical and mental health. Aim for 7-9 hours of sleep per night to support your body's natural healing and rejuvenation processes.",
        "Eat a Balanced Diet: Focus on consuming a variety of nutrient-rich foods, including fruits, vegetables, lean proteins, whole grains, and healthy fats. This helps ensure you get essential vitamins and minerals for optimal health.",
        "Move Your Body: Incorporate regular physical activity into your routine. Whether it's walking, jogging, yoga, or weightlifting, aim for at least 30 minutes of exercise most days of the week to support cardiovascular health, muscle strength, and mental well-being.",
    ]
}

```

# Step 2:

```swift
struct WaterWidgetView : View {
    var entry: WaterProvider.Entry
    
    var body: some View {
        VStack(alignment: .leading){
            HStack{
                Image(systemName: "drop")
                Text("Tip of the day")
            }
            
            .font(.title3)
            .bold()
            .padding(.bottom, 8)
            
            Text(entry.waterTip)
                .font(.caption)
            
            Spacer()
            
            HStack{
                Spacer()
                Text("**Last Update:** \(entry.date.formatted(.dateTime))")
                    .font(.caption2)
                    
            }
        }.foregroundStyle(.white)
        .containerBackground(for: .widget){
            Color.cyan
        }
    }
}
```

# Step 3: 

```swift

struct WaterProvider: TimelineProvider {
    private let waterTips = Tips()
    private let placeholderEntry = WaterEntry(
        date: Date(),
        waterTip: ""
    )
    
    func placeholder(in context: Context) -> WaterEntry {
        return placeholderEntry
    }
    

    func getSnapshot(in context: Context, completion: @escaping (WaterEntry) -> ()) {
        completion(placeholderEntry)
    }
    
    func getTimeline(in context: Context, completion: @escaping (Timeline<WaterEntry>) -> Void) {
        let currentDate = Date()
        var entries : [WaterEntry] = []
        for minuteOffset in 0 ..< 60 {
            let entryDate = Calendar.current.date(byAdding: .minute, value: minuteOffset, to: currentDate)!
            let entry = WaterEntry(date: entryDate, waterTip: waterTips.tipsList[Int.random(in: 0...waterTips.tipsList.count-1)])
            entries.append(entry)
        }
        
        let timeline = Timeline(entries: entries, policy: .atEnd)
        completion(timeline)
    }

}

```

# Step 5:

```swift
struct WaterEntry: TimelineEntry {
    let date: Date
    let waterTip: String
}
```

# Step 6: 

```swift
@main
struct AwesomeQuoteWidget: Widget {
    let kind: String = "AwesomeQuoteWidget"

    var body: some WidgetConfiguration {
        StaticConfiguration(
            kind: kind,
            provider: WaterProvider(),
            content: { WaterWidgetView(entry: $0) }
        )
        .configurationDisplayName("Quote of the day")
        .description("Quotes that change your life!")
        .supportedFamilies([.systemMedium, .systemLarge])
    }
}


#Preview(as: .systemMedium) {
    AwesomeQuoteWidget()
} timeline: {
    WaterEntry(date: .now, waterTip: "Hello")
    WaterEntry(date: .now + 1, waterTip: "Hello!")
}

```
