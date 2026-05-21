# introduction

Wireshark is an:
- open source
- cross platform
- packet analyzer

used for:
- capturing packets
- inspecting network traffic
- analyzing PCAP files


# tool overview

wireshark use cases
- detect network problems
- analyze suspicious traffic
- learn protocol behavior
- investigate anomalies

improtant: wireshark is not an IDS

it only captures and analyzes packets

# wireshark interface sections
main sections:
1. toolbar
2. filter bar
3. packet list pane
4. packet details pane
5. packet bytes pane

capture file comment flag
```
path:
statistics -> capture file properties

```
# packet dissection
packet dissection

wireshark breaks packets into protocol layers:
- ethernet
- ip
- tcp
- http
- etc

this helps inspect:
- headers
- payloads
- protocol data

# packet navigation
navigation features

useful options:
- go to packet
- find packets
- packet comments
- expert info

# packet filtering
packet filtering help isolate packets

example: http

shows only http traffic

# important filtering feature
apply as filter
steps:
1. right click protocol
2. apply as filter
3. selected protocol filter appears

# important concepts
|concept |meaning |
|--------|--------|
|pcap |packet capture file |
|ttl |time to live |
|payload |actual transmitted data |
|filter |show specific packets |
|stream |full communication flow |

# important wireshark features
| feature | purpose |
|---------|---------|
|packet list |shows all packets |
|packet details |protocol breakdown |
|packet bytes |raw hexadecimal data |
|filters |search traffic |
|expert info |warnings/errors |

# imprortant filters 
| filter | purpose |
|--------|---------|
|http |http traffic |
|tcp |tcp packets |
|dns |dns traffic |
|ip.addr == x.x.x.x |filter ip |
|tcp.port == 80 |filter port |

