# Forwarding and Routing
## Forwarding
- Forwarding involved the transfer of a packet from an incoming link to an outgoing link **WITHIN** a **SINGLE ROUTER**
- Each router has a **forwarding table**

## Routing
- Routing involves all the routers in the network where the collective interactions via routing protocols will determine the path that the packet will take to get from the source to the destination
- The algorithm that is used to determine the route or path that is taken by the packets as they are flowing is referred to as **routing algorithms**

# Internet Protocol (IP)
The purpose of the internet protocol (IP) is a set of *communications protocol* that is used for relaying datagrams across network boundaries. There are services that is provided by IP that will be discussed in more depth in this document.

Services:
1. [Fragmentation and Reassembly](#Fragmentation-and-Reassembly)
2. Addressing
3. Forwarding

## Fragmentation and Reassembly

Below will list the datagram format for IPv4
1. Version : IPv4/IPv6
2. Header Length: Length of the header of a particular packet.
3. Types of Service : Differentiated Services Code Point (DSCP), used to differentiate/prioritize the packets of various services.
4. Datagram Length : Total length of packet in bytes. Min of 20 bytes and max of 60 bytes.
5. 16-bit identifier: Used for fragmentation and reassembly
6. Flags: 3-bit flag used to indicate whether any fragments are expected (fragmentation)
7. Fragment offset: represents the number of data bytes ahead of a particular fragment in the specific datagram. (fragmentation)
8. Time-to-live: 8-bit field that indicates the maximum time the datagram will be live in the Internet system
9. Upper-layer protocol: 8-bit field that represents the transport layer protocol that handed over data to the network layer
10. Header checksum: Used to check for data integrity

Fragmentation is when one big datagram gets split into smaller packets to travel through the network and then finally reassembled at the finals destination.

MTU: Maximum Transfer Unit

Example 1
4000 Byte Datagram , MTU = 1500 bytes, Size of header = 20 bytes
|ID| Length|Fragmentation Flag | Offset |
|---|---|---|---|
|X|1500|1|0|
|X|1500|1|185|
|X|1060|0|370|

Length of datagram is obtained by adding the length of the data that is divisible by 8 and the size of the datagram.
The fragmentation flag will be set to true if there are still fragments after the respective packet that is currently being processed.
Offset is calculated by dividing the length of the data by 8 and that is the offset of the packet. Each successive packet should have a cumalative amount of offset.

Example 2
6020 bytes Datagram, MTU = 1600 bytes , size of header = 20 bytes
|ID| Length|Fragmentation Flag | Offset |
|---|---|---|---|
|X|1596|1|0|
|X|1596|1|197|
|X|1596|1|394|
|X|1312|0|591|

## IP Addressing
### IP Classicification (Classful addressing)
![classful]()
Class A: 0.0.0.0 - 127.255.255.255
Class B: 128.0.0.0 - 191.255.255.255
Class C: 192.0.0.0 - 223.255.255.255
Class D: 224.0.0.0 - 239.255.255.255
Class E: 240.0.0.0 - 255.255.255.255

IP addresses are split into different classes as we can see above, and the first 4 bits are used to identify which class the IP address is classified under.

**Special Addresses**
- 0.x.y.z - Usually a source address that is used as part of the network initialization process, eg. the Dynamic Host Configuration Protocol (DHCP) uses 0.0.0.0 by hosts that are requesting for IP addresses.
- 127.x.y.z - Usually a internal loopback address for a network device. 127.0.0.1 is commonly used for testing and developmental purposes
- 255.255.255.255 - Limited broadcast address within a subnet


