# TCP Vegas: New Techniques for Congestion Detection and Avoidance

## Abstract

Vegas is a new implementation of TCP that achieves between 40 and 70% better throughput, with one-fifth to one-half the losses, as compared to the implementation of TCP in the Reno distribution of BSD Unix. This paper motivates and describes the three key techniques employed by Vegas, and presents the results of a comprehensive experimental performance study—using both simulations and measurements on the Internet—of the Vegas and Reno implementations of TCP.

## 3.2 Congestion Avoidance Mechanism

TCP Reno’s congestion detection and control mechanism uses the loss of segments as a signal that there is congestion in the network. It has no mechanism to detect the incipient stages of congestion—before losses occur—so they can be prevented. Reno is reactive, rather than proactive, in this respect. As a result, Reno *needs* to create losses to find the available bandwidth of the connection. This can be seen in Figure 6, which shows the trace of a Reno connection sending 1MB of data over the network configuration seen in Figure 5, with no other traffic sources; i.e., only Host1a sending to Host1b. In this case, the router queue size is ten and the queuing discipline is FIFO.

There are several previously proposed approaches for proactive congestion detection based on a common understanding of the network changes as it approaches congestion (an excellent development is given in [7]). These changes can be seen in Figure 6 in the time interval from 4.5 to 7.5 seconds. One change is the increased queue size in the intermediate nodes of the connection, resulting in an increase of the RTT for each successive segment. Wang and Crowcroft’s DUAL algorithm [11] is based on this increase of the round-trip delay. The congestion window normally increases as in Reno, but every two round-trip delays the algorithm checks to see if the current RTT is greater than the average of the minimum and maximum RTTs seen so far. If it is, then the algorithm decreases the congestion window by one-eighth.

Jain’s CARD (Congestion Avoidance using Round-trip Delay) approach [7] is based on an analytic derivation of a socially optimum window size for a deterministic network. The decision as to whether or not to change the current window size is based on changes to both the RTT and the window size. The window is adjusted once every two round-trip delays based on the product *(WindowSize_current - WindowSize_old) × (RTT_current - RTT_old)* as follows: if the result is positive, decrease the window size by one-eighth; if the result is negative or zero, increase the window size by one maximum segment size. Note that the window changes during every adjustment, that is, it oscillates around its optimal point.

Another change seen as the network approaches congestion is the flattening of the sending rate. Wang and Crowcroft’s Tri-S scheme [10] takes advantage of this fact. Every RTT, they increase the window size by one segment and compare the throughput achieved to the throughput when the window was one segment smaller. If the difference is less than one-half the throughput achieved when only one segment was in transit—as was the case at the beginning of the connection—they decrease the window by one segment. Tri-S calculates the throughput by dividing the number of bytes outstanding in the network by the RTT.

Vegas’ approach is most similar to Tri-S, in that it looks at changes in the throughput rate. However, it differs from Tri-S in that it calculates throughputs differently, and instead of looking for a change in the throughput slope, it compares the measured throughput rate with the expected throughput rate. The simple idea that Vegas exploits is that the number of bytes in transit is directly proportional to the expected throughput, and therefore, as the window size increases—causing the bytes in transit to increase—the throughput of the connection should also increase.

Vegas uses this idea to measure and control the amount of *extra* data this connection has in transit, where by extra data we mean data that would not have been sent if the bandwidth used by the connection exactly matched the available bandwidth of the network. The goal of Vegas is to maintain the “right” amount of extra data in the network. Obviously, if a connection is sending too much extra data, it will cause congestion. Less obviously, if a connection is sending too little extra data, it cannot respond rapidly enough to transient increases in the available network bandwidth. Vegas’ congestion avoidance actions are based on changes in the estimated amount of extra data in the network, and not only on dropped segments.

We now describe the algorithm in detail. Note that the algorithm is not in effect during slow-start. Vegas’ behavior during slow-start is described in Section 3.3.

First, define a given connection’s *BaseRTT* to be the RTT of a segment when the connection is not congested. In practice, Vegas sets *BaseRTT* to the minimum of all measured round trip times; it is commonly the RTT of the first segment sent by the connection, before the router queues increase due to traffic generated by this connection. If we assume that we are not overflowing the connection, then the expected throughput is given by:

*Expected = WindowSize / BaseRTT*

where *WindowSize* is the size of the current congestion window, which we assume for the purpose of this discussion, to be equal to the number of bytes in transit.

Here is the exact text from your image converted into Markdown — all wording, punctuation, and formatting preserved exactly:

Second, Vegas calculates the current *Actual* sending rate. This is done by recording the sending time for a distinguished segment, recording how many bytes are transmitted between the time that segment is sent and its acknowledgement is received, computing the RTT for the distinguished segment when its acknowledgement arrives, and dividing the number of bytes transmitted by the sample RTT. This calculation is done once per round-trip time.³

Third, Vegas compares *Actual* to *Expected*, and adjusts the window accordingly. Let *Diff = Expected - Actual.* Note that *Diff* is positive or zero by definition, since *Actual > Expected* implies that we need to change *BaseRTT* to the latest sampled RTT. Also define two thresholds, α < β, roughly corresponding to having too little and too much extra data in the network, respectively. When *Diff < α*, Vegas increases the congestion window linearly during the next RTT, and when *Diff > β*, Vegas decreases the congestion window linearly during the next RTT. Vegas leaves the congestion window unchanged when *α < Diff < β.*

Intuitively, the farther away the actual throughput gets from the expected throughput, the more congestion there is in the network, which implies that the sending rate should be reduced. The β threshold triggers this decrease. On the other hand, when the actual throughput rate gets too close to the expected throughput, the connection is in danger of not utilizing the available bandwidth. The α threshold triggers this increase. The overall goal is to keep between α and β extra bytes in the network.

Because the algorithm, as just presented, compares the difference between the actual and expected throughput rates to the α and β thresholds, these two thresholds are defined in terms of KB/s. However, it is perhaps more accurate to think in terms of how many extra *buffers* the connection is occupying in the network. For example, on a connection with a *BaseRTT* of 100ms and a segment size of 1KB, if α = 30KB/s and β = 60KB/s, then we can think of α as saying that the connection needs to be occupying at least three extra buffers in the network, and β saying it should occupy no more than six extra buffers in the network.

In practice, we express α and β in terms of buffers rather than extra bytes in transit. During linear increase/decrease mode—as opposed to the slow-start mode described below—we set α to two and β to four. This can be interpreted as an attempt to use at least two, but no more than four extra buffers in the connection.

Figure 7 shows the behavior of TCP Vegas when there is no other traffic present; this is the same condition that Reno under in Figure 6. There is one type of graph in this figure, the time line, which depicts the congestion avoidance mechanism (CAM) used by Vegas. Once again, we use a detailed graph (Figure 8) keyed to the following explanation:

1. The small vertical line—once per RTT—shows the times when Vegas makes a congestion control decision; i.e., computes *Actual* and adjusts the window accordingly.

2. The gray line shows the *Expected* throughput. This is the throughput we should get if all the bytes in transit are able to get through the connection in one *BaseRTT.*

3. The solid line shows the *Actual* sending rate. We calculate it from the number of bytes we sent in the last RTT.

4. The dashed lines are the thresholds used to control the size of the congestion window. The top line corresponds to the α threshold and the bottom line corresponds to the β threshold.

Figure 9 shows a trace of Vegas sharing the bottleneck router with *tcplib* traffic. The bottom graph shows the output produced by the TRAFFIC protocol simulating the TCP traffic. The thin line is the sending rate in KB/s as seen in 100ms intervals; the thick line is a running average (size 3). The graph clearly shows Vegas’ congestion avoidance mechanisms at work and how its throughput adapts to the changing conditions on the network.
