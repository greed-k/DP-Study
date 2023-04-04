# Transport Layer Services
- The transport layer in the OSI model is the lowest level that supports end-to-end protocols
- The transport layer adds functionality to the best-effor packet delivery IP service

There are 2 commonly used protocols that exists. They are
- [UDP](#UDP)
- [TCP](#TCP)
Both protocols provides different features that will suit different use cases. 
# UDP
## Description 
*UDP* ( User Datagram Protocol ) 
Unreliable , unordered style of delivery. The goal of UDP is to priortize sending data with lesser delay in mind and it is unable to guarantee that the data that is sent will arrive.
- UDP is a "barebones" internet transfer protocol
	- Allows it to be best effort
	- Segments may be lost during transfer or out-of-order
- UDP is **connectionless** 
	- Does not maintain connections between sender and receiver
	- Each UDP message is independent
Examples of apps that uses UDP as its protocol of choice for transfer 
- DNS
- Gaming 
- VPN

## Why UDP?
-  There is no need for connection establishment ( adds delay )
-  Simple
-  Smal header size
-  No congestion control : allows full speed sending of data from sender to receiver

## UDP Segment

![UDPSegment](https://github.com/greed-k/DP-Study/blob/master/CSD%202160%20(Networking)/images/udpSegment.png)

## UDP Checksum
***CHECKSUM*** : Addition of segment content
### Sender
- Treats the contents segment as a sequence of 16-bit integers
- Sender computes the checksum value into the UDP checksum field
### Receiver
- Compute the received content's checksum
- Cross check the computed checksum value against the checksum field value
- If values do not match, the content has been modified

# TCP
*TCP* : Transmission Control Protocol
Reliable, in-order delivery. 
- Using **flow control**, **sequence numbers** , **acknowledgements** , and **timers**, TCP can ensure that the data that being sent over the network is sent over in order and also correct.
- TCP employs **congestion control** to prevent any one TCP connection from overloading the links and routers with an excessive amount of traffic.
- TCP also aims to give each connection a **equal** amount of bandwidth regardless of how congested the network traffic might be.

Even with all these features of TCP, there are drawbacks with the protocol the drawbacks are as listed.
- **Longer** delays
	- Due to the way the protocol works, it prioritizes reliable data transfer over speed, hence there are some delays introduced when using the protocol which allows it to ensure the data that is being sent and received is guaranteed and also correct.
- Lacks minimum throughput gurantee
	- Similar to the issue above, with the protocol having to ensure reliable delivery, it is unable to guarantee a minimum throughput.
- Lacks security
	- TCP is a connection oriented protocol, and there are no forms of security that is put in place to ensure what data is being sent is fully secure.
## TCP Segment

![TCPSegment](https://github.com/greed-k/DP-Study/blob/master/CSD%202160%20(Networking)/images/tcpSegment.png)

## TCP Flags
|Name | Definition|
|-------|-------|
|**URG**|Urgent data flag. When set, the priority of the packet is set as high and the server should process it ASAP.|
|**ACK**|Acknowledgement flag. This flag is used to indicate that the Acknowledge Number Field in the TCP header is significant.|
|**PSH**|Push flag. The flag is used to tell the **RECEIVER** to push the data to the application as soon as possible instead of buffering the data.|
|**RST**|Reset flag. The flag is used to indicate that the connection should be reset. Used to indicate an error or to terminate an established connection.|
|**SYN**|Sync flag. The flag is used to initiate a new connection or sync sequence numbers. When set the device is either trying to establish a connection or resync an exisiting connection.|
|**FIN**|Finish flag. The flag is used to indicate that the sender has no more sender has no more data to send and is trying to close the connection.|

## TCP connection management 
Connection management is essential for TCP, which is a connection oriented protocol. It provides function such as connection establishment and connection termination. In order to facilitate this, the sender and receiver will have a "handshake". 
Handshaking of the sender and receiver refers to: 
- Agreement to establishment of connection where both parties are aware that they are establishing the connection.
- Connection parameters to be agreed on.
- Ensure that there will be no ambiguity between the client and server when the connection has opened.
### TCP 3-way handshake

![3way](https://github.com/greed-k/DP-Study/blob/master/CSD%202160%20(Networking)/images/3wayHandshake.png)

### TCP Sequence number & Acknowledgement number
The sequence number (***SEQ***) for a segment is the byte-stream number of the **first** byte in the segment.

Eg.
