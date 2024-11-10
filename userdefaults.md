# UserDefaults

Rules:

1. First Store Data
2. Then Retrieve Data

```

// Storing a Boolean preference for notifications
UserDefaults.standard.set(false, forKey: "notificationsEnabled")

// Retrieving the notifications preference
let notificationsEnabled = UserDefaults.standard.bool(forKey: "notificationsEnabled")
print("Notifications enabled: \(notificationsEnabled)")

```

1. That constant can be named anything
2. You cans store any type of data, you just have to just say it


# Storing Custom Objects With Codable

First:

Conform to Codable

```

struct UserSettings: Codable {
    var username: String
    var notificationsEnabled: Bool
    var themePreference: String
}

```

1. If this was your struct, and you wanted to store this using UserDefaults, you MUST conform it to Codable

Next

Storing a Custom Object

```

let userSettings = UserSettings(username: "Fahim", notificationsEnabled: true, themePreference: "dark")

if let encodedData = try? JSONEncoder().encode(userSettings) {
    UserDefaults.standard.set(encodedData, forKey: "userSettings")
}


```

1. Create an instance of your struct
2. encodedData can be named anything but typically people use encodedData so do the same
3. You refer to your custom data type where you see userSettings
4. You can name the key whatever


Next

Retrieving a Custom Object

```

if let savedData = UserDefaults.standard.data(forKey: "userSettings"),
   let decodedSettings = try? JSONDecoder().decode(UserSettings.self, from: savedData) {
    print("Username: \(decodedSettings.username)")
    print("Notifications Enabled: \(decodedSettings.notificationsEnabled)")
    print("Theme Preference: \(decodedSettings.themePreference)")
}


```

1. That if let is necessary and the only thing you should change in a different situation is the key if you were referring to something else
2. let is also necessary and so is the .self 
