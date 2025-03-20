## Commit 1 Reflection notes
The handle_connection function in Rust processes an incoming TCP stream by reading HTTP request headers. It starts by creating a BufReader to efficiently handle stream data, then reads the request line by line using .lines(). The .map(|result| result.unwrap()) extracts the actual string, and .take_while(|line| !line.is_empty()) ensures only the headers are captured before collecting them into a Vec. Finally, it prints the request using println!("Request: {:#?}", http_request);, providing a structured debug output.

This function demonstrates efficient buffered reading and line-by-line parsing of an HTTP request. However, using .unwrap() can lead to panics if errors occur, so a more robust error-handling approach would be beneficial. The function is a foundational component of a basic HTTP server, helping to parse requests before processing and responding accordingly.

## Commit 2 Reflection notes
![Image - 1](/static/image1.png)

## Commit 3 Reflection notes
![Image - 2](/static/image2.png)
The refactoring process improves code clarity and organization by separating request handling and response selection. In the previous implementation, the code read the entire HTTP request into a vector and then proceeded directly to responding with a fixed file. This approach did not distinguish between different requests, always returning the same file regardless of what was requested.

The refactored version improves upon this by extracting only the first line of the request, which contains the method and requested path. By checking if the request matches "GET / HTTP/1.1", the function can determine whether to return the main page or a 404 response. This makes the server more dynamic, allowing different responses based on the request. Additionally, the refactoring simplifies the code by removing unnecessary collection, repeatable code and iteration over request lines, making it more efficient and easier to maintain.
