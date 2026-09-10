# OSI model - 7 layers

what is osi model?
- the osi model(open systems interconnection) is a 7 layer framework that explains how data travels from one system to another.

think of it as a step by step journey of data

7. application
6. presentation
5. session
4. transport
3. network
2. data link
1. physical

# 7 layers of osi model

|layer name |example |
|-----------|--------|
|application |http, ftp |
|presentation |encryption |
|session |session management |
|tansport |tcp/udp |
|network |ip |
|data link |mac |
|physical |cables |

7. Appliation layer
- topmost layer of osi model and closest to the end user
- provides interface for users and software application to interact with the network
- handles high level function like file transfers, email and web browsing

what it does:
- user interacts here

example:
- web browsing
- email
- file transfer

protocols:
- http/https
- ftp
- smtp 

soc perspective:
- phishing attacks
- malicious urls
- suspicious api calls

6. presentation layer
- this layer is responsible for translation, encryption, and compression of data
- it ensures that data sent from the application layer is in a format that can be understood by the receiving system
- handles tasks like data formating, character encoding (e.g, ASCII to unicode) and data encryption

what it does:
- data formatting
- encryption / decryption

examples:
- ssl/tls
- encoding

soc perspective:
- encryption analysis
- ssl stripping (MITM)

5. Session layer 
- this layer establishes, manages and terminates sessions between two communicating devices
- ensures that data exchange is synchronized and allows applications to communicate effectively without interference

what it does:
- maintains session between systems

example:
- login session
- session cookies

soc perspective:
- session hijacking
- token reuse

4. transport layer
- segments the data received from the upper layer 
- proides error detection and correction
- ensures the reliable delivery of data between two devices across a network
- it controls flow to prevent congestion and guarantees that data is delivered in the correct order

what it does:
- end to end communication
- reliablility

protocols:
- tcp (reliable)
- udp (fast, unrealiable)

soc perspective:
- port scanning
- syn flood attacks
- suspicious ports

3. network layer
- it determines the best path to send data across multiple networks
- handles logical addressing and routing, enabling data to travel from one network to another, regardless of the physical infrastructure
- routers operate at this layer, forwarding data between different networks based on ip addresses

what it does:
- routing
- ip addressing

protocol:
- ip (ipv4/ipv6)

soc perspective:
- ip tracking
-  geolocation
- suspicious external connections

2. data link layer
- this layer sits above the physical layer and is responsible for the reliable transfer of dat across a physical network link
- this layer ensures that data is error-free and properly framed for transmission
- it also manages how devices on the same local network communicate with each other

what it does:
- mac address communciation
- local network delivery

soc perspective:
- ARP spoofing (MITM)
- mac anomalies

1. physical layer
- deals with the actual transmission of raw binary data (1s and 0s) over a physical medium, such as cables, fiber optics, or wireless signals

what it does:
- hardware transmission
- electrical signals

soc perspective:
- rarely used directly
- but important in hardware attacks

# How does communication happen in the OSI Model
Communication in the OSI Model follows a systematic process called Encapsulation and Decapsulation:

1. Sender’s Side:
● Data is generated at the application layer and moves downward through the layers.
● Each layer adds its own header, and sometimes a footer, encapsulating the data with layer-specific information (e.g., addressing, error checks).

2. Transmission:
● The encapsulated data (now called a packet) is transmitted over the physical medium to the receiving device.

3. Receiver’s Side:
● The process is reversed as data moves upward through the OSI layers.
● Each layer removes its corresponding header/footer (decapsulation) until the original data is presented to the receiving application.

Note : This structured approach ensures data integrity and reliability, even over complex networks

# TCP/IP model (real-world model)
what is tcp/ip model?
- it is a simplified version of osi, used in real networks(internet)

5. application layer
4. transport layer
3. internet layer
2. data-link layer
1. physical layer

# tcp/ip layers
|TCP/IP Layer |maps to osi |
|-------------|------------|
|Application |osi 7,6,5 |
|Transport |osi 4 |
|Internet |osi 3 |
|Network Access |osi 2,1 |

4. application layer
includes:
- http
- https
- dns 
- ftp

soc view:
- phishing
- dns attacks
- api abuse

3. transport layer
protocols:
- tcp
- udp 

soc view:
- port scanning
- syn flood
- traffic anomalies

2. internet layer
protocol:
- ip

soc view:
- suspicious ip
- external communication
- botnet traffic

1. network access layer
includes:
- mac 
- ARP
- ethernet

soc view:
- ARP spoofing
- internal attacks

# Soc example (mapping)
alert:
- suspicious login via https from unknown ip

analysis:
- application -> http login
- transport -> port 443
- network -> external ip
- data link -> internal network

# soc analyst thinking
whenever you see a log, break it like:
- which layer is involved?

example:
- port issue -> transport
- ip ussue -> network
- dns issue -> application
- arp issue -> data link

