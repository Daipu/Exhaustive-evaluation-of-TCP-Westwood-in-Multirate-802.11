# Exhaustive-evaluation-of-TCP-Westwood-in-Multirate-802.11

## Course Code: CS821

## Overview

TCP Westwood[1][2] is a TCP extensions proposed mainly for wireless networks. ns-3 has inbuilt models for TCP westwood. This project aims to evaluate the performance of TCP Westwood in the presence of Rate Adaptation Algorithms such as ARF, AARF, AARF-CD, ONOE and Minstrel

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

### For TCP Westwood should be executed as
 
./waf --run "scratch/2_AP-4_wifi-sta --wifiManager=Aarf --tcpVariant=TcpWestwood" --vis

### If you want a graph between Throughput and time Then use this command  

./waf --run "scratch/2_AP-4_wifi-sta --wifiManager=Aarf --tcpVariant=TcpWestwood --pcap=true" --vis

When we do pcap=true then we get a pcap file in Exhaustive-evaluation-of-TCP-Westwood-in-Multirate-802.11 directory and we convert that pcap file to plot file using a python script.

### After that we pass plot file to Gnuplot with below command 

plot "file_name.plotme" using 1:2 title "Base" with line 

that will give us a plot between throughput ann time.that gives a graph between throughput and time.


# References
[1] Saverio Mascolo, Claudio Casetti, Mario Gerla, M. Y. Sanadidi, and Ren Wang (2002). TCP Westwood: End-to-End Congestion Control for Wired/Wireless Networks.  

[2] Naeem Khademi, Michael Welzl, and Renato Lo Cigno. TCP Westwood: End-to-End Congestion Control for Wired/Wireless Networks  

