### __client-server processes__ :-

Whenever a new client connects to the server, making a new child process for each new client. 

Layers:-
 - Application 
 - transport 
 - network
 - link layer 
 - physical layer

 ## __Socket__
A socket is a `software endpoint that enables two-way communication between devices over a network.` Think of it as a virtual plug that connects two machines so they can talk to each other.

It’s defined by a combination of `IP address + port number`

`Used heavily in client-server models (e.g., web browsers talking to web servers)`

NOTE: TCP and UDP require different sockets as :-

`Stream Socket (TCP)`
Connection-oriented
Reliable, ordered data transfer
Like a phone call: both sides stay connected during the conversation

`Datagram Socket (UDP)`
Connectionless
Faster but no guarantee of delivery
Like sending letters: no confirmation if they arrive

`127.0.0.1:8080`


## __What is logical communication endpoint(SOCKET) ?__

- Think of it like a virtual `“address”` for a conversation between two computers or programs.

- the communication start's and end.
It doesn’t mean a physical wire or cable, but rather a software-defined endpoint that uniquely identifies a connection.

- When two devices talk over the internet, each `endpoint` is defined by:
`IP address + Port number`

- `192.168.1.5 → the device (server)`
`443 → HTTPS service`


## __What is a port?__
A Port is a logical communication endpoint in a computer’s network stack that helps differentiate multiple applications or services running on the same machine.

-` Well-known ports` (e.g., HTTP: 80, HTTPS: 443, FTP: 21)
`Registered ports`
`Dynamic/private ports`

- `If your computer (with IP 192.168.1.5) opens a connection to Google’s server (172.217.14.206:443) at port 443, the socket looks like:`

```scss
(192.168.1.5, 52345) → (172.217.14.206, 443)
```
- `52345 is a random local ephemeral port` selected by your operating system.

## __TCP/IP and Sockets__
- The OS manages a socket table to track all active connections.
- Connection Process (TCP):
Client opens a socket → Requests connection to server's IP & Port.
TCP performs a 3-way handshake:

## connection from same ip + same port :-

```
Connection	Client IP	Client Port        Server IP	        Server Port
1	192.168.1.5	          52345	           172.217.14.206	      80
2	192.168.1.6	          52346	           172.217.14.206	      80
3	192.168.1.7	          52347	           172.217.14.206	      80
```

## __Socket gloabally unique ?__
-`A Socket is globally unique on the network level because the combination of:`
`Client IP + Client Port +
Server IP + Server Port
produces a globally unique identifier.`

### __Teleconferencing__
- way for multiple people in different locations to connect using phone lines, video, or the Internet

- syntax - format,structure.
- symantic - logic,intent,behaviour.

## __interoperability:-__
 - the ability of computer system's or software to exchange and make use of information.

