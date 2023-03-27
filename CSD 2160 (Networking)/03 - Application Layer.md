# Client-Server
---
## Client
The *client* process is the  one that initiates the communication to the server. This is typically something like a web browser that is waiting to connect to a webpage.

A client's characteristics is as follows:
- Is able to communicate with a server
- Typically intermittently connects to a server as it is unable to always keep a stable constant connection to a server due to many factors such as delays.
- May have dynamic IP that is assigned to the clients depending on the network that they are connected to.
- Do not communicate with other clients directly

## Server
The *server* process it the one that is waiting for the clients to contact it and send back responses. The server is the one that stores and contains all the files that a client is looking to access.

A servers characteristics is as follows:
- Always on host
- Hosted on a well known IP address and/or domain name.
- Hosted on a well known port number

## Sockets
Sockets provides an application with a standardized way to send and receive messages over the internet without having to know the low-level details.

Below shows an image that explains the basic role of a socket

![Socket](https://github.com/greed-k/DP-Study/blob/master/CSD%202160%20(Networking)/images/socket.png)

All processes have a unqiue identifier to allow the process to interface with the socket and send or receive messages. The identifier includes a *unique* 32-bit IP address and port number that is associated with the process.

### Examples:
Example port numbers
- HTTP server: 80
- Mail server : 25
To send HTTP message to ict.singaporetech.edu.sg web server:
- IP Address :128.119.245.12
- Port number: 80

### Message Definitions
In a tytpical HTTP message that is about to be sent out by a client, it will contain the following information:
- Type of message : Request, Response
- Message Syntax : What fields in messages and how fields are delineated
- Message semantics : The meaning of the information in the fields
- Rules :  When and how the processes can send and respond to messages that are being sent and receiving.

### Transport Layer Services 
Below lists some services that are required by an app when using a socket
- Data Integrity
	- Some apps requires 100% reliable data transfer ( file transfer , web transactions)
	- Some apps can tolerate losses ( streaming audio or video )
- Timing (Latency)
	- Some apps require low amounts of delay to work effectively 
		- eg. Games, Video Chatting, Internet Phone Calls
- Throughput
	- Amount of bandwidth/ throughput that an app can get
	- Some apps (video streaming ) requires a certain amount of throughput to be effective
	- Other apps are able to make use of whatever throughput that they get
- Security 
	- Some apps need encryption and data integrity
		- eg. Web transactions, Online banking


---
# Socket Programming
