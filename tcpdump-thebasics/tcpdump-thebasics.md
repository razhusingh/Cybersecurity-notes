# introduction

Tcpdump
tcpdump is a command-line packet analyzer used to:
- capture packets
- read pcap files
- filter traffic
- analyze network communication

it uses: libpcap
library for packet capturing

# learning objectives 
this room teaches:
- capturing packets
- saving captures
- reading pcap files
- applying filters
- displaying packets properly

# basic packet capture
list interfaces
```
command:
tcpdump -D
shows available interfaces
```
capture on interface
```
command:
tcpdump -i eth0
-i = interface
captures live traffic
```
disable name resolution
```
command:
tcpdump -n

purpose
- prevent hostname resolution
- show raw ip addresses
- faster output
```
limit captured packets
```
command;
tcpdump -c 5

- -c = capture count
- stops after specified packets
```
save capture to file
```
command:
tcpdump -w capture.pcap

- -w = write packets to file 
```

Read pcap file
```
command:
tcpdump -r capture.pcap

```
# filtering traffic
filter by host
```
command:
tcpdump host 1.1.1.1

captures packets:
- to 
- from
specified host
```
filter by source host
```
command:
tcpdump src host 1.1.1.1
```
filter by destination host
```
command:
tcpdump dst host 1.1.1.1

```
filter by port
```
command:
tcpdump port 80
```
filter by source port
```
command:
tcpdump src port 443
```
filter by destination port
```
command:
tcpdump dst port 53
```
filter by protocol
```
tcp
tcpdump tcp

udp
tcpdump udp

icmp 
tcpdump icmp
```
combine filters
```
and
tcpdump tcp and port 80

or
tcpdump port 80 or port 443

not 
tcpdump not icmp

```
# ARP analysis
ARP = Address resolution protocol

used to : ip -> mac resolution

Display arp packets
```
command:
tcpdump arp
```
read arp from pcap
```
command:
tcpdump -r traffic.pcap arp

example arp query
who has 192.168.1.1?
tell 192.168.1.10
```
# display options
verbose output

```
verbose
tcpdump -v

more verbose
tcpdump -vv

maximum verbosity
tcpdump -vvv
```
Show ASCII output
```
command:
tcpdump -A

displays
ASCII packet contents
```
Show hexadecimal output
```
command:
tcpdump -x

displays:
hex packet data
```

show link layer headers
```
command:
tcpdump -e

shows:
- mac addresses
- ethernet headers
```

useful combination
```
command:
tcpdump -nn -r file.pcap

meaning:
- -n = no hostname resolution
- second -n = no port-name resolution

shows:
raw ips and raw port numbers
```
# important tcpdump syntax
Common Options Summary
|Option |Purpose |
|-------|--------|
|-i	|Select interface |
|-n	|Disable name resolution |
|-r	|Read PCAP |
|-w	|Write PCAP |
|-c	|Packet count |
|-v	|Verbose |
|-A	|ASCII output |
|-x	|Hex output |
|-e	|Ethernet headers |

Common Filters Summary
|Filter	| Purpose |
|host x.x.x.x	|Specific host |
|src host	|Source host |
|dst host	|Destination host |
|port 80	|Specific port |
|tcp	|TCP traffic |
|udp	|UDP traffic |
|icmp	|ICMP traffic |
|arp	|ARP packets |

Important Commands Summary
|Command | Purpose |
|tcpdump -D	|List interfaces |
|tcpdump -i eth0	|Capture on interface |
|tcpdump -r file.pcap	|Read capture |
|tcpdump -w file.pcap	|Save capture |
|tcpdump tcp	|TCP traffic |
|tcpdump arp	|ARP packets |

