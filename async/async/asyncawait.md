#Async/Await

async and await aren’t specifically for creating delays—they’re for managing asynchronous tasks.

Asynchronous tasks are operations that take time to complete, like:

Fetching data from a server
Loading large files
Waiting for user input


# Example: Calling an Async Function with Task

```

func fetchData() async -> String {
    return "Fetched Data"
}

// Trying to call fetchData() in regular code:
Task {
    let data = await fetchData()
    print(data)
}

```

1. That async marks fetchData as a asynchronous function and uif you want one you always have to do that
2. async func are special because you cant call them like real functions, you must call them with Task as shown

3. # Example: Fetching Two Pieces of Data Asynchronously

```

import Foundation

func fetchUserProfile() async -> String {
    try? await Task.sleep(nanoseconds: 1_000_000_000) // 1 second delay
    return "User Profile Data"
}

func fetchUserActivity() async -> String {
    try? await Task.sleep(nanoseconds: 1_500_000_000) // 1.5 second delay
    return "User Activity Data"
}

func fetchUserData() async {
    // Fetch both pieces of data using await
    let profileData = await fetchUserProfile()
    let activityData = await fetchUserActivity()
    
    // Process the fetched data together
    print("Fetched Data: \(profileData) and \(activityData)")
}

Task {
    await fetchUserData()
}


```
1. fetchUserProfile and fetch userActivity basically are asynchronous functions thats simluate a delay when in reality you would have your code so when the cloud finally fetches the data you would return but this is for example purposes
2. fetchUserData nests both of them and both those constants basically say wait until we recive fetchUserProfile and the fetchUserActivity and then print
3. Task is just what you gotta do to run it because async funcs are special

# Example: Fetching Data Concurrently


```
import Foundation

func fetchUserProfile() async -> String {
    try? await Task.sleep(nanoseconds: 1_000_000_000) // 1 second delay
    return "User Profile Data"
}

func fetchUserActivity() async -> String {
    try? await Task.sleep(nanoseconds: 1_500_000_000) // 1.5 second delay
    return "User Activity Data"
}

func fetchUserDataConcurrently() async {
    // Start both async tasks concurrently using async let
    async let profileData = fetchUserProfile()
    async let activityData = fetchUserActivity()

    // Wait for both tasks to complete and gather the results
    let profile = await profileData
    let activity = await activityData
    
    print("Fetched Data: \(profile) and \(activity)")
}

Task {
    await fetchUserDataConcurrently()
}
```

1. Yes this achieves the samething as above BUT its faster, this is called concurrent execution while the above is sequentioal execution
2. There are only Four new lines of code and they have been marked with a comment and removed only two from the previous one
3. By using async let, we’re telling Swift to start both fetchUserProfile() and fetchUserActivity() at the same time, without waiting for either to finish before starting the other.


Sequential Execution (earlier example):

1. fetchUserProfile() runs first and takes 1 second.
2. Once it’s done, fetchUserActivity() starts and takes 1.5 seconds.
3. Total time: 1 second + 1.5 seconds = 2.5 seconds.

   
Concurrent Execution (current example):

1. fetchUserProfile() and fetchUserActivity() start at the same time.
2. fetchUserProfile() finishes in 1 second, and fetchUserActivity() finishes in 1.5 seconds.
3. Total time: Since they run at the same time, you only wait for the longest task, which is 1.5 seconds.

So, while the final output is the same, concurrent execution can save time, especially when the tasks are independent and can run side by side.
