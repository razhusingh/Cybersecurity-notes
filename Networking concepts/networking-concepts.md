# Introduction 
what is networking?

- communication between devices
- enables data transfer over networks

why important in cybersecurity?

- attacks happen over networks
- understanding traffic = detecting threats

# osi(open systems interconnection) model
Definition
- A conceptual model that explains how data travels across a network using 7 layers

OSI layer(top -> bottom)
| layer | name | function | example protocols and standards |
|-------|------|----------|---------------------------------|
|7 |application |user interaction (HTTP, FTP) | http, ftp, dns, pop3, smtp, imap |
|6 |presentation |encryption, encoding | unicode, MIME, jpeg, png, mpeg |
|5 |session |session management |nfs, RPC |
|4 |transport |end to end delivery (TCP/UDP) |UDP, TCP |
|3 |Network |routing(ip) |IP, ICMP, IPSec |
|2 |data link |mac address, local delivery |ethernet (802.3), wifi(802.11) |
|1 |physical |cables, signals |electrical, optical, and wireless signals |

memory trick
- please do not throw sausage pizza away

Key points
- routing -> layer 3
- encryption -> layer 6
- TCP/UDP -> layer 4
- same network -> layer 2

# TCP/IP model
Definition
- Real world networking model (simplified osi)

layers
| TCP/IP layer | OSI equivalent |
|--------------|----------------|
|application |5,6,7 |
|transport |4 |
|internet |3 |
|network access |1,2 |

key points 
- HTTP -> application layer
- used in real network

# IP addressing
what is ip?
- unique identifier for devices
- example: 192.168.1.1

looking up your network configuration
- ipconfig
- ipconfig a s (address show)

types

Private IP
- 10.0.0.0 - 10.255.255.255
- 172.16.0.0 - 172.31.255.255
- 192.168.0.0 - 192.168.255.255

public IP
- used on the internet

key concepts
- ip = logical address
- MAC = physical address

# TCP vs UDP

TCP(transmission control protocol)
- reliable
- connection based
- uses 3 way handshake

tcp is established using three way handshake. two flags are used: syn(synchronise) and ack(acknowledgment). the packet are sent as follows:

1. syn packet
2. syn-ack
3. ack packet

examples
- http, https

UDP(user datagram protocol)
- fast
- no connection
- no guarantee

examples
- streaming, gaming

comparison
| feature | TCP | UDP |
|---------|-----|-----|
|speed |slow |fast |
|reliability |high |low |
|connection |yes |no |


# Encapsulation
Definition
process of adding headers to data as it moves down the network layer

steps:
1. application layer
- data is created by the user/application
raw data

2. transport layer
- tcp -> segment
- UDP -> datagram
port number are added

3. network layer
- Ip address is added
data becomes -> packet

4. data link layer
- mac address is added
final form -> frame

data units
|layer | data name |
|------|-----------|
|transport(tcp) |segment |
|transport(udp) |datagram |
|data link |frame |

key points 
- data changes form at each layer
- frame used in local network

final flow
- data -> segment/datagram -> packet -> frame

# extra
when receiving
- frame -> packet -> segment -> data

this is called de-encapsulation

# Telnet (teletype network)
what is telnet?
- tool to connect to remote systems 
- used for testing port/services

command
telnet <ip> <port>

uses 
- check open ports
- banner grabbing

# final summary

| topic | key idea |
|-------|----------|
|osi model |7 layer |
|tcp/ip |4 layer |
|IP address |device identity |
|tcp | reliable |
|udp | fast |
|encapsulation |data wrapping|
|telnet |remote conncetion |
