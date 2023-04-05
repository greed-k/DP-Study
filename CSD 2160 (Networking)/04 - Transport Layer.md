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

The acknowledgement number (**ACK**) is a number that is retrived from the message that the current host receives from the other host that it is communicating with.

For better illustration, a diagram will be provided below which is a snippet from the slides.

Eg. 
![seqNack](https://github.com/greed-k/DP-Study/blob/master/CSD%202160%20(Networking)/images/seqNack.png)

As seen from the imgage above, host A types in the character 'C' and it is sent over to host B. 
Host B receives the message, acknowledges the message by taking the sequence number that was used for the previous number to be used as the acknowledge number (**ACK**) to inform the other host when sending back the message that it has already received the message previously. The size of the data is then also factored into the acknowledge number that is being set over, hence why the number changed from 42 to 43.

The sequence number that is used for host B to send back the message will then be the acknowledge number that was previously sent over from host A.

### Closing a TCP connection

![closingTCP](https://github.com/greed-k/DP-Study/blob/master/CSD%202160%20(Networking)/images/closeTCP.png)

Steps that is followed by the protocol to close the connection.
1. Client will send a message containing the flag **FIN** set to 1.
2. Server receives the message, sends back another message with the **ACK** bit in the TCP segment structure set to 1, and the ACK number that is sent back will be the sequence number +1 from the **FIN** bit.
3. Server will also close their connection from the client, then repeating something similar, where the sever will send a message this time with the **FIN** flag set to 1 in the TCP segment structure and sent back to the client
4. The client will repeat what the server has done previously, sending a TCP segment structure with the **ACK** bit set to 1, and the **ACK** number will take the sequence number that was sent from the server's message and adding the 1 to the number that is from the **FIN** bit that was set previously  by the server.

### Reliable Data Transfer
There are some methods that are employed by TCP to ensure that the data that it is transmitting between 2  users are reliable. Below will list the methods.
1. Pipelined segments
2. Cummulative acks
3. Retransmission timer

In an event of retransmission, the protocol will only do so when the following happens.
1. Timeout events
2. Duplicate acks

Below attached will be images that show off the different scenarios
- LOST ACK 

![lost-ack](https://github.com/greed-k/DP-Study/blob/master/CSD%202160%20(Networking)/images/lost-ack.png)

- PREMATURE TIMEOUT

![premature-timeout](https://github.com/greed-k/DP-Study/blob/master/CSD%202160%20(Networking)/images/premature-timeout.png)

- CUMULATIVE ACK

![cumulative-ack](https://github.com/greed-k/DP-Study/blob/master/CSD%202160%20(Networking)/images/cumulative-ack.png)

- FAST RETRANSMIT

![fast-retransmit](https://github.com/greed-k/DP-Study/blob/master/CSD%202160%20(Networking)/images/fast-retransmit.png)
