 ## Websocket :-
 - in simple req and res cycle the when client get's response the connection closes. 
 - as server also dont' send data by itself (ah in some cases server push is a feature but it's limited and less).
  so in a chat app if the if the client1 send's message to server than how client2 will retrieve it? 

  - 1.` it can continuosly send request of asking if there any message for me in each second. but it will just increase the load on server bad practice. it is ``polling`.

  - 2. `it can use an upgrade header within it's http req and ask the server to upgrade this connection to Websocket. server will respond and there is open connection now server many req within same time no need of req from the client. and the same client can push once client done it can close the connection.`

  ### `server sent events `:-
  - in server sent events the server keep pushing the data it's one way communication. ex - tv,broadcast.

  ## Websocket API 
  - full duplex(two-way) communication protocol.
  - the programming interface that let's a developers use the websocket protocol. 
  - in browser this webSocket class in js.
  - the protocol is websocket.
  - `The WebSocket API is the WebSocket object + methods/events (onopen, onmessage, send, close, etc.) that allow you to use the protocol in code`.

  - __note__: in simple http server can only send res once client sent req.