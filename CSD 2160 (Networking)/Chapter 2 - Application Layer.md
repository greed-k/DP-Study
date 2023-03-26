# Web and HTTP
---
## HTTP Overview

**HTTP** : Hypertext Transfer Protocol
HTTP falls under the the **Application Layer Protocol** and it uses a **Client-server Model**.  Examples of where HTTP can be used are things such as entering a video call, where the initial hand shake of the client and server is done using the HTTP protocol.

### Client Server Model

1. **Client** : A device that is capable of using the HTTP protocol, eg. from a browser, that requests receieves and "displays" web objects. ( Using TCP or UDP )
2. **Server** : Web server is responsible for sending beack objects that are in response to the requests that are made to the server.

![[Pasted image 20230326202141.png]]
src : https://www.researchgate.net/figure/TCP-IP-layered-protocol-communication-between-two-end-point-devices-Functionally_fig1_310317068

### TCP 
The TCP protocol is protocol that is part of the transport layer.
- Example:
	-  Initiate TCP connection to server (Client)
	-  TCP connection accepted ( Server )
	-  HTTP messsages are exchanged between the client and server.
	-  TCP connection closes.
