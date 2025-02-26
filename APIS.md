
# APIS

# Steps: 
1. Define data models exactly as how the JSON file has it
2. Make a func with comepletion type and return void
3. Use @escaping to have it be async
4. Create a URL
5. Use URLSession.shared.dataTask(with:) to create a task.
6. Handle Errors
8. Decode Data
9. Call .resume() to actually start the network request.

```swift

Step 1: Define Data Models
// Define data models exactly as how the JSON file has it, also need to conform to this protocol
struct Post: Codable, Identifiable {
    let id: Int
    var title: String
    var body: String
}

Step 2: Create API Class
class Api {
    // Step 3: Make a function with a completion handler that returns Void, notice the array
    func getPosts(completion: @escaping ([Post]) -> Void) {
        
        // Step 4: Create a URL
        guard let url = URL(string: "https://jsonplaceholder.typicode.com/posts") else {
            print("Invalid URL")
            return
        }
        
        // Step 5: Use URLSession.shared.dataTask(with:) to create a task
        let task = URLSession.shared.dataTask(with: url) { data, response, error in
            
            // Step 6: Handle Errors
            if let error = error {
                print("Error fetching posts: \(error.localizedDescription)")
                return
            }
            
            guard let data = data else {
                print("No data received")
                return
            }
            
            do {
                // Step 7: Decode Data
                let posts = try JSONDecoder().decode([Post].self, from: data)
                
                // Step 8: Use DispatchQueue.main to update UI on the main thread
                DispatchQueue.main.async {
                    completion(posts)
                }
            } catch {
                print("Decoding error: \(error.localizedDescription)")
            }
        }
        
        // Step 9: Call .resume() to actually start the network request
        task.resume()
    }
}
```
# Display data in swift 

```swift

struct PostListView: View {
    @State private var posts: [Post] = [] // Stores fetched posts
    
    var body: some View {
        NavigationView {
            List(posts) { post in
                VStack(alignment: .leading) {
                    Text(post.title)
                        .font(.headline)
                    Text(post.body)
                        .font(.subheadline)
                        .foregroundColor(.gray)
                }
            }
            .navigationTitle("Posts")
            .onAppear {
                // Call API function to fetch posts(gotta do this!)
                Api().getPosts { fetchedPosts in
                    self.posts = fetchedPosts
                }
            }
        }
    }

```


# Resources 
[APIS](https://medium.com/@kmarion76/what-is-an-api-and-how-do-i-use-it-in-swift-d43f136517e7)
