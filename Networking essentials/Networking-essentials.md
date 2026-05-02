# Introduction

Networking
- devices communicate with each other
- internet = network of networks

# DHCP: give me my network settings

DHCP(dynamic host configuration protocol)

purpose
automatically assigns:
- ip address
- subnet mask
- default gateway
- dns server

DHCP process (DORA)
|step |meaning |
|-----|--------|
|discover |device searches dhcp server |
|offer |server offers ip |
|request |device requests ip |
|acknowledge |server confirms |

important 
without DHCP:
- manual ip configuration needed

# ARP: bridging layer 3 addressing to layer 2 addressing
ARP(Address resolution protocol)

purpose
converts:
- ip address -> mac address

example 
192.168.1.5 -> oo:1A:2B:3C:4D:5E

key point
- ip = layer 3
- mac = layer 2

arp connects both

# ICMP: troubleshooting networks

ICMP(Internet control message protocol)

purpose
- error reporting
- network troubleshooting

ping
used for connectivity testing

example:
ping google.com

traceroute
shows packet path

windows:

tracert google.com

linux:

traceroute google.com

# routing
process of forwarding packets between networks

Router
purpose
- connects networks
- forwards packets

default gateway
router ip used to access external networks

example:
192.168.1.1

routing table

contains:
- destination network
- next hop
- interface

# NAT (Network address translation)

purpose
converts:
- private ip -> public ip

benefits
- saves public ip addresses
- adds basic privacy

example
- 192.168.0.137 -> 212.3.4.5

PAT
Port address translation

uses:
- one public ip
- multiple port numbers

important
approx tcp ports:
- 0 - 65535

# key concepts

- dhcp assigns ip addresses

- arp resolves ip to mac

- icmp used for troubleshooting

- routers forward packets

- nat converts private ip to public ip