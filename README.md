# Application Setup
Clone the repo       
cd server (In vscode terminal)           
npm install          
npm run dev (keep the server running)                    
cd client (In different terminal of vscode)                           
npm install                
npm start       

note: In order to test multiple users follow:
       1) Please open react app in 2 different browsers or in 2 different tabs.
       2) Use different user names and same Room number (ex: if user1 starts room number 1 , in order to join the chat with user1 user2 must also put room number as 1) 
Here You can see the exchange of messages.  




# Description of the application's architecture
## 1)Express.js Server:

* The index.js file initializes an Express application instance and creates an HTTP server using this instance.
* CORS middleware is enabled to allow cross-origin requests.
* Incoming request bodies are parsed as JSON.
* The server listens on a specified port (defaulting to 3002) for incoming requests.
## 2)WebSocket Integration:
* The socketSetup function in socket.js sets up WebSocket connections.
* Upon a new connection (connection event), a unique socket ID is logged, and listeners are set up for various events:
* join_room: A client requests to join a room. Upon receiving this event, the server adds the socket to the specified room and logs the event.
* send_message: A client sends a message. The server logs the message content and emits a receive_message event to all sockets in the specified room, containing the message content.
* disconnect: Triggered when a client disconnects, and it logs a disconnection message.
## 3)Concurrency Handling:
* In the Express.js server setup, each incoming HTTP request is handled in its own context.
* Express itself handles concurrency within the scope of HTTP request handling, but it's mainly designed for handling multiple requests simultaneously.
* With WebSocket connections, Socket.IO manages concurrency for WebSocket communication. Each WebSocket connection runs in its own event loop, and Socket.IO handles the concurrency internally. Events like join_room, send_message, and disconnect are managed per socket connection, ensuring that concurrent requests from different clients are processed appropriately.


