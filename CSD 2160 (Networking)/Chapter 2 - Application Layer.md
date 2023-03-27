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
- Properties
	-  One object sent over at a time over the TCP connections
	- Connection is closed after the exchange
	- When downloading objects, **MULTIPLE** connections are required.
- Issues
	- Requires 2 [RTT](#response-time--rtt-) to send each web object.
	- OS has to allocate overhead for each TCP connection.
	- Browsers commonly open parallel TCP connections to getch referenced objects.


#### Persistent Connections ( HTTP 1.1 )
- Properties
	- Multiple objects sent over a single TCP connection between the client and server.
	- Pipelining of requests.
- Advantages over non-persistent
	- Server leave connection open after sending a response
	- Subsequent HTTP messages between same client/server sesnt over open connection
	- Client sends requests as soon as it encounters a referenced object
	- As little as one RTT for **ALL** referenced objects
### Response Time ( RTT )

Response Time ( RTT ) refers to the time for a small packet to travel from client to the server and back. 

Transmission time refers to the time take for a small packet to be streamed or emitted into the medium.

**FORMULA** : 
$$ t_{reponse} =  2RTT + t_{transmission}$$

- $t_{response}$  :  Non-Persistent HTTP response time
- $RTT$  :  Each Response time cycle timing
- $t_{transmission}$  : File Transmission Time 
### Network Delays 
#### Transmission Delay
- Properties
	- Caused due to end system injecting data buts into the network
	- Eg : Imagine pouring a cup of water into a pipe. It takes a finite amount of time for you to empty the cup.
	- This can be lowered by having a bigger bandwidth that is available to the network
- **FORMULA** 
	- *$$d_{transmission} = \frac{L}{R}$$
	- L : Data Size
	- R : Bandwidth
#### Propagation Delay
- Properties
	- Caused due to taking a finite amount of time to travel across a given distance
	- Eg: Imagine water being poured though a pipe and the time that it takes for the water to move from end to end.
	- This is determined by the total distance that the data has to travel to get to its destination.
- **FORMULA** 
	- $$d_{propagation} = \frac{d}{s}$$
	- d : Distance
	- s : Propagation Speed
#### Node Delay 
- Properties
	- This is an additional delay that is experienced by the packet throughout its transmission over the network, as the packet will be passed from the client and throught a series of nodes and overall distance before it can reach its destination.
	-  In node delay, there are additional delays that have to be considered also. All delays that have to be considered to calculate the node delay is listed below
		- Process Delay ( $d_{process}$  ) 
		- Queue Delay ( $d_{queue}$ )
		- Transmission Delay ( $d_{transmission}$ )
		- Propagation Delay ( $d_{propagation}$ )
- **FORMULA** 
$$d_{node} = d_{process} + d_{queue} + d_{transmission} + d_{propagation}$$
### HTTP Modeling
Assuming that a webpage consists of
- 1 Base HTML page ( Size O )
- M images ( Each Size O )




## FORMULAS
| Name | Formula |
| -------- | ------- |
|Response Time| $t_{reponse} =  2RTT + t_{transmission}$|
|Transmission Delay| $d_{transmission} = \frac{L}{R}$|
|Propagation Delay| $d_{propagation} = \frac{d}{s}$|
|Node Delay | $d_{node} = d_{process} + d_{queue} + d_{transmission} + d_{propagation}$|


