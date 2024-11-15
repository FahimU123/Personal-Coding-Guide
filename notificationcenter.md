# NotificationCenter

# UserNotification

```

import UserNotifications

```

```

func requestNotificationPermission() {
        UNUserNotificationCenter.current().requestAuthorization(options: [.alert, .sound, .badge]) { granted, error in
            if granted {
                print("Notification permission granted!")
            } else if let error = error {
                print("Error: \(error.localizedDescription)")
            }
        }
    }

```

1. This code requests permission to actually send notifications
2. If else statemnt isnt necessary and can be replaved with { _, _ in } instead of granted and error

```

  func scheduleDailyNotification() {
        let content = UNMutableNotificationContent()
        content.title = "Daily Reminder"
        content.body = "Don't forget to check the app today!"
        content.sound = .default

        let trigger = UNTimeIntervalNotificationTrigger(timeInterval: 60, repeats: true)
        
        let request = UNNotificationRequest(identifier: "vyu", content: content, trigger: trigger)
        
        UNUserNotificationCenter.current().add(request) { error in
            if let error = error {
                print("Error scheduling notification: \(error.localizedDescription)")
            }
        }
    }

```


1. This is to schedule them
2. timeInterval is in seconds
3. repeats decide if this will repeat every 60 sencods or just do the noti that one time
4. I dont fully get request but you need it so the request can be packaged and sent to UNUserNotificationCenter
5. The identifier can be anything but name it carefully as you will use this to refer back tot his noti if you wnat to update it later
