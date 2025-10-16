# NETWORK ANALYSIS : Analyzing captured packets using Wireshark.

---

## Lab overview

This lab contains an already captured SBT-PCAP file for network traffic analysis with Wireshark on a Linux machine. This lab is for anyone in the SOC, Network/Digital Forensic or any path that involves monitoring of networks.

## Goal and scope

I am to perform the following activities on the PCAP capture given.

1. Which protocol was used over port 3942?
2. What is the IP address of the host that was pinged twice?
3. How many DNS query response packets were captured?
4. What is the IP address of the host which sent the most number of bytes?

## Environment & Prerequisites

- OS (Windows/Mac/Linux)
- Wireshark([https://www.wireshark.org/download.html](https://www.wireshark.org/download.html)) install

Open Wireshark and import the pcap file

![image.png](NETWORK%20ANALYSIS%20Analyzing%20captured%20packets%20using%20%2028c2ec062bfd802589d6f7bc75bf2a97/image.png)

from the drop down menu under the “File” select “Open” and find the path to which the captured file is.

## PCAP Analyses Methodology (workflows and techniques)

### Objectives/Questions

1. Which protocol was used over port 3942?

![image.png](NETWORK%20ANALYSIS%20Analyzing%20captured%20packets%20using%20%2028c2ec062bfd802589d6f7bc75bf2a97/image%201.png)

### Answer : SSDP

To identify the protocol used on the captured related port 3942, we use the filter 

```
tcp.port == 3942 || udp.port == 3942
```

This filter allows us to view traffics associated with either TCP or UDP transport protocols. From the “Protocol” session in the details, we can identify the exact protocol used on port 3942.

1. What is the IP address of the host that was pinged twice?

![image.png](NETWORK%20ANALYSIS%20Analyzing%20captured%20packets%20using%20%2028c2ec062bfd802589d6f7bc75bf2a97/image%202.png)

### Answer : 8.8.4.4

A ping utility is a command used to test the reachability of a device on a network. It uses the ICMP (Internet Control Message Protocol) echo request(i.e from ip_address 192.168.1.7) and echo reply(i.e ip_address 8.8.4.4) packets between the hosts.

1. How many DNS query response packets were captured?

![Screenshot 2025-10-16 033954.png](NETWORK%20ANALYSIS%20Analyzing%20captured%20packets%20using%20%2028c2ec062bfd802589d6f7bc75bf2a97/Screenshot_2025-10-16_033954.png)

Using the “dns” filter in the display filter column, we can “right-click” on the DNS Flag Response message in the “Packet Headers” and “Apply as Filter” as shown in the diagram above. This technique selects all DNS response query.

![image.png](NETWORK%20ANALYSIS%20Analyzing%20captured%20packets%20using%20%2028c2ec062bfd802589d6f7bc75bf2a97/image%203.png)

### Answer : 90

In the “display filter” menu, we were able to see the filter that can be applied manually, i.e 

```
dns.flags.response == True
```

The results of the filter gives us the number of DNS query response in the captured pcap file.

1. What is the IP address of the host which sent the most number of bytes?

![image.png](NETWORK%20ANALYSIS%20Analyzing%20captured%20packets%20using%20%2028c2ec062bfd802589d6f7bc75bf2a97/image%204.png)

### Answer : 115.178.9.18

To find the IP address, go to “Statistics” at the top menu and select “Endpoint” in the drop down menu. In the new open window, we can select “IPv4” option and follow the “Tx Bytes” column to find the IP address along with the most number of bytes transmitted.

> NOTE : Rx packets are received by the device whiles Tx packets are transmitted by the device.
> 

## Thank you.