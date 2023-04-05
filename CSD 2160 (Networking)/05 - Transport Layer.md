# Error Control
## Stop-and-Wait
- •Packet is sent **one** at a time. 
- If **ACK** is received, the next packet is sent.
- If **ACK** is not received, resend after timeout.

## Go-Back-N
- **N** number of packets can be sent based on window size. 
- Once the window size is exhaust, it will wait for **ACK** to send more packets
- Receiver only receives packets that are in order. All out-of-order packets are **discarded**.

## Selective Repeat
 -  **N** number of packets can be sent based on window size. 
 - Receiver **ACK** all packets received correctly regardless if it is in order. 
 - **ACK** with cumulative **ACK** and bitmap of packets received correctly.

How are the above methods used to help achieve error control? Below are three mechanisms that is put in place to implement it.
1. Error detection using the checksum
2. Positive acknowledgement
3. Timeout

If there are damaged packets that are detected,  all packets sent after the damaged packet will all have to be resent. ( GO-BACK-N )

Loss is detected with the following methods
- Timeout
- Duplicated Acknowledgements

### TCP Timer
- Retransmission
	- Defines the maximum time to wait before packets are considered as lost
	- $$Retransmission time = 2*RTT$$
	- $$RTT = \alpha * RTT_{previous} + (1 - \alpha) * RTT_{current}$$
- Persistence
	- Timer set out and receiver will wait for the window size announcement
	- If timer goes off a probe segment will be sent to the source
	- Persistent timer is then changed to a retransmission time
	- If no response received, timer is reset and the timer value is doubled
	- If timer hits the maximum threshold of 60s and does not double
	- One probe segement is then sent everey 60 seconds until the window size is received as the response 
- 
- Keepalive
	- Prevent long idle connections between 2 TCP
	- Timer is reset whenever server receives a segment from the client
	- If no activity happens for 2 hours, a probe segment will be sent
	- After 10 probes, 75s apart, if client does not respond, it is assumed to be down.
- Time-waited
	- Used in connection termination
	- After TCP closes connection is held in limbo for time waited periods
	- Value of timer is 2 times the lifetime of the segment

# Efficiency
$$a = \frac{t_{propagation}}{t_{packet}}$$
## Stop-and-Wait
$$Efficiency = \frac{t_{packet}}{t_{packet} + 2t_{propagation}} = \frac{1}{1+2a}$$
## Go-Back-N
$$Efficiency = \frac{N * t_{packet}}{t_{packet} + 2t_{propagation}} =\frac{N}{1+2a}$$

# Flow Control
- Why is it needed?
	- To help regulate the data flow that a receiving transport entity will receieve.
	- Too much data might be sent to the entity at one point which can cause the receiving entity to have the buffer overflowed.
- Approached to flow control
	- Do nothing
		- Transfer Protocol data unit (**TPDU**) will allow the overflow and the overflown data will be lost
	- Refuse to accept packets from the network layer
		- At the network layer, a **backpressure** mechanicsm is implemented where a "choke" packet is received. When received, the choked packet will be sent back to the original source instead of being placed in the buffer to be processed.
	- By using one of the error control methods menthioned above. (Sliding window)
		- By holding acknowledgements at one end, the sending side which can be configured to resend packets after a certain time will send the packet again .
		- The source doesn not need to send a full window's worth of data
		- The size of the window can be increased or decreased by the destination
		- Destination can send back an acknowledgement anytime

# Congestion Control
Congestion happens due to the rapid growth of the internet. Congestion of internet traffic causes packet loss and the losses leads to re-transmissions. These retransmissions if not regulated will fill the traffic and cause the network to collapse.

Below in the subsections lists the 3 techniques that is being used by TCP to help regulate congestion control.
1. Slow start
2. Implements additive increase
3. multiplicative decrease algorithm to change window size

Slow start employs 3 phases in trasmitting data to help control the amount of outbound network
- Slow Start Phase
	- Slow exponential increments to the threshold (ssthresh)
	- Starts with one window and exponential increase when an ACK is received
	- increase the amount of cwnd each time exponentially (Congestion Window)
		- by $cwnd^2$ 
- Congestion Avoidance Phase
	- Linear additive increase of 1 cwnd after the threshold for the slow start is reached
	- After each ACK, $cwnd = cwnd + 1$ 
- Congestion Detection Phase
	- Depending on the case, if there is congestion that is detected, the sender will either be sent back to slow start or congestion avoidance
	- Congestion is detected from the loss of packets
	- Apply multiplicative decrease algo to change window size

![SlowStart](https://github.com/greed-k/DP-Study/blob/master/CSD%202160%20(Networking)/images/slow-start.png)

In the detection phase, there are 2 cases that can happen which are discussed below
1. Retransmission due to **Timeout** 
	1. ssthresh is reduced to **HALF** of the **current** window size
	2. Reduce the number of cwnd back to 1
	3. Start back at slow start phase again
	4. slow phase will work up back to the new ssthresh and then go back to the congestion detection phase
2. Retransmission due to **3 DUPLICATE** acknowledgements
	1. ssthresh is reduced to **HALF** of the **current** window size
	2. cwnd is set to ssthresh 
	3. start at congestion avoidance phase

![case1](https://github.com/greed-k/DP-Study/blob/master/CSD%202160%20(Networking)/images/case1-timeout.png)

![case2](https://github.com/greed-k/DP-Study/blob/master/CSD%202160%20(Networking)/images/case2-dupe.png)

# TCP Segment Options
Usually **20** bytes, but can contain up to **40** bytes and at the end of the option there is one byte that will signify end-of-option.

There is a maximum segment size that can be defined during the connection setup. this value can be up to 2 bytes in value

**Window Scale Factor** defines the scaling size of the window
This can be used to determine how much data can be sent with the given data rate. The window can then be resized according to the formula given below
- $$Size_{NewWindow} = Size_{window} * 2^{Scale_{window}}$$
$$Scale_{window} = log_2\frac{Size_{NewWindow}}{Size_{window}}$$
Timestamp in the options is then used to compute the round trip delay (**RTD**)

