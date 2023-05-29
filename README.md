# **Part2**

 1. When q = 20, the average fetch time for 3 fetches is 0.84106s, and the standard deviation is 0.78981s
When q = 100, the average fetch time for 3 fetches is 3.97283s, and the standard deviation is 1.9795s

2. The difference in webpage fetch times with short and large router buffers is attributed to the bufferbloat phenomenon. With a small buffer size, such as 20, the queue at the bottleneck quickly fills up but also empties promptly, resulting in relatively low latency. If the queue becomes full, packets are dropped, triggering congestion control mechanisms. The small buffer size leads to frequent drops and multiplicative decreases in sending rate, resulting in a stable sending rate.
In contrast, a larger buffer size, like 100, takes longer to fill, allowing the sender to increase its sending rate. The increased buffering introduces higher latency as more packets need to be emptied. The latency decreases only when the queue becomes full, packets are dropped, and the sender initiates multiplicative decrease. Due to the larger buffer size, there are fewer multiplicative decreases, leading to a more variable sending rate.
The discrepancy in webpage fetch times can also be attributed to the behavior of TCP congestion control algorithms. TCP aims for full utilization of links by increasing the congestion window until a packet is dropped when the output buffer at the bottleneck is full. With a longer queue, packets of new TCP connections for webpage fetches wait longer in the queue, resulting in prolonged fetch times.

3. The maximum transmit queue length is 1000, with a MTU of 1500 Bytes.

    1500 * 8 * 1000 / 100 / 10^6 = 0.12 seconds

&nbsp;
4. When the queue size is set to 20, the round-trip time (RTT) remains small, ranging from 100ms to 250ms. This narrow range can be attributed to the effectiveness of TCP congestion control mechanisms. When the queue size is small, regular packet drops occur, leading to frequent multiplicative decreases and maintaining a relatively stable sending rate. This is reflected in the compressed nature of the RTT graph for the queue size of 20.
On the other hand, when the queue size is increased to 100, the RTT experiences a significant rise and a broader range of 100ms to 1600ms. With fewer packet drops occurring due to the larger buffer, there are fewer multiplicative decreases in the sending rate. As a result, the RTT values become more varied and extended.
Overall, a queue size of 20 maintains a small and stable RTT range due to regular packet drops and multiplicative decreases. In contrast, a queue size of 100 leads to a higher and more diverse RTT range as fewer packet drops occur, resulting in fewer multiplicative decreases.

5. 
 - Active Queue Management: Have the switch tell the sender the current status of the queue; For instance, if it is close to congestion. This can be done using ECN, which the switch detects the onset of congestion. When congestion is detected, it marks affected packets. The receiver of the marked packets than informs the sender using a congestion signal.
 
 - BBR: BBR uses an algorithm that responds to congestion, rather than packet loss. BBR tackles this with a ground-up rewrite of congestion control. BBR considers how fast the network is delivering data. For a given network connection, it uses recent measurements of the network's delivery rate and round-trip time to build an explicit model that includes both the maximum recent bandwidth available to that connection, and its minimum recent round-trip delay. BBR then uses this model to control both how fast it sends data and the maximum amount of data it's willing to allow in the network at any time.
