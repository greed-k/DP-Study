# Web and HTTP
---
## HTTP Overview

**HTTP** : Hypertext Transfer Protocol
HTTP falls under the the **Application Layer Protocol** and it uses a **Client-server Model**.  Examples of where HTTP can be used are things such as entering a video call, where the initial hand shake of the client and server is done using the HTTP protocol.

### Client Server Model

1. **Client** : A device that is capable of using the HTTP protocol, eg. from a browser, that requests receieves and "displays" web objects. ( Using TCP or UDP )
2. **Server** : Web server is responsible for sending beack objects that are in response to the requests that are made to the server.

![OSI Model](https://github.com/greed-k/DP-Study/blob/master/CSD%202160%20(Networking)/osi.png)

src : https://www.researchgate.net/figure/TCP-IP-layered-protocol-communication-between-two-end-point-devices-Functionally_fig1_310317068

### TCP 
The TCP protocol is protocol that is part of the transport layer.
- Example:
	-  Initiate TCP connection to server (Client)
	-  TCP connection accepted ( Server )
	-  HTTP messsages are exchanged between the client and server.
	-  TCP connection closes.

### Persistent and Non-Persistent Connections

#### Non-Persistent Connection ( HTTP 1.0 )
- One object sent over at a time over the TCP connections
- Connection is closed after the exchange
- When downloading objects, **MULTIPLE** connections are required.

#### Persistent Connections ( HTTP 1.1 )
- Multiple objects sent over a single TCP connection between the client and server.
- Pipelining of requests.

### Response Time ( RTT )

