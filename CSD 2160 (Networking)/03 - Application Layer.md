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



---
# Socket Programming
