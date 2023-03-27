# Web and HTTP
---
## HTTP Overview

**HTTP** : Hypertext Transfer Protocol
HTTP falls under the the **Application Layer Protocol** and it uses a **Client-server Model**.  Examples of where HTTP can be used are things such as entering a video call, where the initial hand shake of the client and server is done using the HTTP protocol.

### Client Server Model

1. **Client** : A device that is capable of using the HTTP protocol, eg. from a browser, that requests receieves and "displays" web objects. ( Using TCP or UDP )
2. **Server** : Web server is responsible for sending beack objects that are in response to the requests that are made to the server.

![OSI Model](https://github.com/greed-k/DP-Study/blob/master/CSD%202160%20(Networking)/images/osi.png)

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
$$t_{reponse} =  2RTT + t_{transmission}$$

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
	- $$d_{transmission} = \frac{L}{R}$$
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

All schemes of HTTP modeling includes transmission time of $(M + 1)*\frac{O}{R}$ where R is the response time.

1. Non-Persistent HTTP:
	- M + 1 TCP connections in series
	- Response time = M + 1 times the time to send an object of size O over a TCP connection.
	- $t_{ResponseTime}=(M+1)*\frac{O}{R}+(M+1)*2RTT$
2. Persistent HTTP with pipelining
	- 2 RTT before beginning to receive base HTML file (1 RTT for TCP, 1 for HTTP)
	- 1 RTT to request and receive M images
	- $t_{ResponseTime}=(M+1)*\frac{O}{R}+3RTT$
3. Non-Persistent , parallel HTTP:
	- Suppose up to X parallel connections; M/X integer. 
	- 1 TCP connection for base file 
	- M/X sets of parallel connections for images.
	- $t_{ResponseTime}=(M+1)*\frac{O}{R}+(\frac{M}{X}+1)*2RTT$
	

---
## HTTP Message

HTTP has support for *self-describing feature* using MIME (Multipurpose Internet Mail Extensions) that informs the server about the data representation that they can understand.

### HTTP Request Message
![HTTP Request Example](https://github.com/greed-k/DP-Study/blob/master/CSD%202160%20(Networking)/images/HTTP_Request_Message.png)

### Uploading form input

#### POST 
- Webpage will include the form input to send to the server
- Input is uploaded to the server in the entity's body of the HTTP request message

#### GET
- Uses the URL mehthod
- The input is embedded into the URL field of request line
- eg: www.somesite.com/animalsearch?animal=monkey%26fruit=banana

#### POST vs GET
- POST
	- *UNLIMITED* amount of data that can be sent to server 
	- Data *GURANTEED* to send to server
	- Requires a form to collect data
- GET
	- Limited to *255* bytes
	- Data can be *INTERCEPTED* by cache proxy
	- Not necessary to use a form. Can be embedded directly into the URL.

### Method Types
- HTTP/1.0 :
	- GET
	- POST
	- HEAD
		- Asks server to leave requested object out of the response
- HTTP/1.1
	- GET, POST , HEAD
	- PUT
		- Uploads file into entity body to path specified in URL field
	- DELETE
		- Deletes file specified in the URL field
- HTTP Response Message:
![HTTP Response Message](https://github.com/greed-k/DP-Study/blob/master/CSD%202160%20(Networking)/images/HTTP_response.png)

- HTTP Response status codes
	- 200 OK
		- Request has succeeded, requested object is inside the response message
	- 400 Bad Request
		- Reqest message is not understood by the server
	- 301 Moved Permanently
		- Requested object moved new location specified later in the response message
	- 404 Not Found
		- Requested document not found on this server
	- 505 HTTP Version Not Supported

---
# Cookies
Cookies is a form of user state retention that is used by websites to store more personal information that is required by the website to function. These information can be things such as the user's login information.

This happens when a user access a site for the first time. When the initial HTTP request arrives at the site, it will ID the user and creates a unique ID and an entry in the backend data base for the ID.

### Components
1. Cookie header line of HTTP response message
2. Cookie header line in next HTTP request message
3. Cookie file kept on user's host , managed by user's browser
4. Back-end database at Website

### Uses 
- Authorization
- Shopping Carts ( E-Commerce )
- Recommendations ( Advertisements )
- User Session State ( Web E-Mail )

### How is the cookie state maintained

Protocol endpoints: maintain state at sender / receiver over multiple transactions
Cookies: HTTP messages carrying the state.


--- 
# Web Caching
### Proxy Server
The goal of a proxy server is to fulfill the proxy request without involving the original server
-  The proxy server is a intermediary server that is located between the client and the original web server. 
- When web caching is implemented through the proxy server, the server is configured to cache the  webpages that are commonly requested by the users. 

Below contains the diagram that shows how the proxy server is commonly configured in a normal  client-server deployment setting.
![Proxy_Server](https://github.com/greed-k/DP-Study/blob/master/CSD%202160%20(Networking)/images/proxy.png)

Caches will be able to act as both a client and server.
- The caches can act as a sort of server to allow for faster access speeds for clients that might be requesting for the pages that they need
- The caches can also be a client to the original server

**Why web caching?**
-  It can help reduce response time for client requests
-  It can help reduce the amount of traffic that is accessing an insitutition's main server
-  Allow for speedier deliver of requests to servers that are of a smaller scale and unable to provide to a large group of users at the same time.

---
# FORMULAS
| Name | Formula |
| -------- | ------- |
|Response Time| $t_{reponse} =  2RTT + t_{transmission}$|
|Transmission Delay| $d_{transmission} = \frac{L}{R}$|
|Propagation Delay| $d_{propagation} = \frac{d}{s}$|
|Node Delay | $d_{node} = d_{process} + d_{queue} + d_{transmission} + d_{propagation}$|
|Non-Persistent HTTP|$t_{ResponseTime}=(M+1)*\frac{O}{R}+(M+1)*2RTT$|
|Persistent HTTP with pipelining|$t_{ResponseTime}=(M+1)*\frac{O}{R}+3RTT$|
|Non-Persistent , parallel HTTP|$t_{ResponseTime}=(M+1)*\frac{O}{R}+(\frac{M}{X}+1)*2RTT$|


