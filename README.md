# Exhaustive-evaluation-of-TCP-Westwood-in-Multirate-802.11

## Course Code: CS821

## Overview

TCP Westwood[1][2] is a TCP extensions proposed mainly for wireless networks. ns-3 has inbuilt models for TCP westwood. This project aims to evaluate the performance of TCP Westwood in the presence of Rate Adaptation Algorithms such as ARF, AARF, AARF-CD, ONOE and Minstrel

##Basic Concepts

###TCP Westwood
 
==> It enhances the performance of TCP window congestion control by using as feedback the end-to-end measurement of the bandwidth
available along a TCP connection.

==> TCP Westwood introduces a mechanism of faster recovery to avoid overly conservative reduction of the congestion window after a
congestion episode by taking into account the end-to-end estimation of available bandwidth. 

==> The available bandwidth is estimated at the TCP source by measuring and low-pass filtering the returning rate of acknowledgments. 

==> The estimated bandwidth is then used to properly set the congestion window and the slow start threshold after a congestion episode, 

that is after a timeout or 3 duplicate acknowledgments.

==> The rationale of this strategy is simple: TCP Westwood sets a slow start threshold and a congestion window which are

consistent with the network capacity measured at the time congestion is experienced.


==> The advantage of the proposed mechanism is that the TCP sender recovers faster after losses especially over connections with large round
trip times, or running over wireless links where sporadic losses are due to unreliable links rather than congestion. 


==> The proposed modifications follow the end-to-end design principle of TCP. They require only slight modifications at the sender side and 

are backward-compatible. Simulation results show a considerable throughput increment in comparison with TCP Reno and TCP SACK over wired 

networks and even more over wireless network.


### Rate Adaptation

Rate adaptation is a criteria that determines the performance of IEEE 802.11 wireless networks, or WiFi. 

Rate adaptation allows transmission to be done at different rates within the wireless network, depending upon the network conditions.

In wireless networks, the signal may be strong or weak. Through rate adaptation technique, the data transfer date can be changed depending upon

the signal strength, i.e. when the signal is strong, high data rates are adopted, while low data rates are adopted during weak signals.


### ARF:: Automatic Rate Fallback

==> In ARF, each sender attempts to use a higher transmission rate after a fixed number of successful transmissions at a given rate and switches back to

a lower rate after 1 or 2 consecutive failures. 


==> Specifically, the original ARF algorithm decreases the current rate and starts a timer when two 

consecutive transmissions fail in a row. 


==> When either the timer expires or the number of successfully received per-packet acknowledgments reaches 10, 

the transmission rate is increased to a higher data rate and the timer is reset.


1. Use a higher rate on every 10 successful transmitted packets.

2. First transmission after rate increase (probing packet) must succeed or rate is immediately decreased and timer is started rather than trying for
second time. 


### AARF:: Adaptive ARF

==> When the transmission of the probing packet fails, we switch back immediately to the previous lower rate (as in ARF) but we also multiply by 

two the number of consecutive successful transmissions (with a maximum bound set to 50) required to switch to a higher rate. 


==> This threshold is reset to its initial value of 10 when the rate is decreased because of two consecutive failed transmissions. 

Reference :: IEEE 802.11 Rate Adaptation: A Practical Approach


### ONOE::

It is a credit based algorithm and tries to find the best data rate with a loss ration less than 50%.

We check credit if it is greater than certain limit then increase the data else decrease the credit.

if credit fall back to certain limit then decrease the data rate.


### Minstrel::


==> Minstrel was intended to address responsiveness and reliability issues with all other rate algorithms available in open-source drivers at the time. 

==> Minstrel is based solely on acknowledgement feedback.

==> Consequently, estimates of future success probabilities at a given rate are based only on past success ratios at that rate.

==> Each decision made in the algorithm has a clear basis, rather than being based on an arbitrary or heuristic choice.

In outline, the algorithm is as follows: A table of acknowledgement
probability estimates is maintained per neighbour per rate. 

On a frequent basis, the table is scanned to find an approximation to the best performing rate and retry chain, and that is used
for transmission for the next interval.

With a moderate frequency, frames are selected to probe presently unused rates, and feedback from those probe frames maintains 
the probability estimates for unused rates so that, should the current best rate deteriorate, there is some basis for immediately selecting
a more successful rate.



## Simulation  

### Performance evaluation of TCPW for multirate 802.11 has been provided in  

scratch/2_AP-4_wifi-sta.cc

we implemented below topology model in 2_AP-4_wifi-sta.cc

                 CSMA Link   
   
       AP1-----------------------------AP2  
      /    \                          /   \                     
     /      \                        /     \                   
    n1      n2                     n3       n4     
   
 
 where AP1 and AP2 are wifi devices and n1, n2, n3, n4 are station devices

### TCP Westwood can be executed as
 
./waf --run "scratch/2_AP-4_wifi-sta --wifiManager=Aarf --tcpVariant=TcpWestwood" --vis     
we can assign any value from these (Aarf, Aarfcd, Amrr, Arf, Cara, Ideal, Minstrel, Onoe, Rraa) value to --wifiManager argument.

### If you want a graph between Throughput and time Then use this command  

./waf --run "scratch/2_AP-4_wifi-sta --wifiManager=Aarf --tcpVariant=TcpWestwood --pcap=true" --vis

When we do pcap=true then we get a pcap file in Exhaustive-evaluation-of-TCP-Westwood-in-Multirate-802.11 directory and we convert that pcap file to plot file using a python script.

### After that we pass plot file to Gnuplot with below command 

plot "file_name.plotme" using 1:2 title "Base" with line 

that will give us a plot/graph between throughput and time.


# References
[1] Saverio Mascolo, Claudio Casetti, Mario Gerla, M. Y. Sanadidi, and Ren Wang (2002). TCP Westwood: End-to-End Congestion Control for Wired/Wireless Networks.  

[2] Naeem Khademi, Michael Welzl, and Renato Lo Cigno. TCP Westwood: End-to-End Congestion Control for Wired/Wireless Networks  

