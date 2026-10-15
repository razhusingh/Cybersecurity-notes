
# Class 34 — Network Traffic Analysis with Wireshark
### 1. 30-Second Recall

- **Network traffic:** Data moving across a network in packets.
- **Encapsulation:** Each network layer adds its own control information.
- **Wireshark:** Open-source packet analyzer used to capture and inspect network traffic.
- **Capture filters:** Select which packets are captured.
- **Display filters:** Hide unwanted packets from the captured traffic without deleting them.
- **TCP handshake:** SYN → SYN-ACK → ACK.
- **TCP Expert Info:** Helps identify retransmissions, duplicate ACKs, and zero-window conditions.
- **Security analysis:** Look for suspicious scan patterns and analyze TLS traffic when session keys are available.

### 2. Must Remember

#### Wireshark Basics
- Capture files: `.pcap` and `.pcapng`.
- Packet List: Displays captured packets.
- Packet Details: Shows decoded protocol fields.
- Packet Bytes: Displays raw packet bytes in hexadecimal and ASCII.
- **Promiscuous Mode:** Captures frames observable by the network interface beyond those addressed to its own MAC, depending on the network setup.
- **Monitor Mode:** Used for Wi-Fi capture.
- **libpcap:** Unix/Linux packet-capture library.
- **Npcap:** Windows packet-capture library; formerly WinPcap.
- **Dissectors:** Decode raw packet bytes into readable protocol information.

#### Capture Filters vs. Display Filters

| Feature | Capture Filter | Display Filter |
|---|---|---|
| When | Before/during capture | After capture |
| Effect | Discards packets that do not match | Hides packets that do not match |
| Syntax | BPF | Wireshark filter syntax |
| Example | `host 192.168.1.1 and port 80` | `ip.addr == 192.168.1.1 && tcp.port == 80` |

#### Important Display Filters

| Purpose | Filter |
|---|---|
| Source IP | `ip.src == 10.0.0.5` |
| Destination IP | `ip.dst == 10.0.0.1` |
| DNS traffic | `dns` |
| HTTP traffic | `http` |
| ARP traffic | `arp` |
| ICMP traffic | `icmp` |
| TLS traffic | `tls` |
| TCP port 443 | `tcp.port == 443` |
| UDP port 53 | `udp.port == 53` |
| Exclude TCP port 80 | `ip.addr == 192.168.1.1 && !tcp.port == 80` |
| HTTP POST requests | `http.request.method == "POST"` |
| DNS query containing a name | `dns.qry.name contains "example"` |

#### Follow Stream and Decode As
- **Follow Stream:** Reconstructs a conversation from packets belonging to a connection, helping inspect sequential payload data.
- **Decode As:** Manually tells Wireshark which protocol to dissect when traffic uses a non-standard port, such as HTTP on port 8080.

#### TCP Three-Way Handshake

| Step | Packet | Sequence/Acknowledgment |
|---|---|---|
| 1 | Client → Server: SYN | Seq = 0 |
| 2 | Server → Client: SYN-ACK | Ack = 1, Seq = 0 |
| 3 | Client → Server: ACK | Seq = 1, Ack = 1 |

After the handshake, the connection state becomes **ESTABLISHED**.

#### TCP Expert Info

- **Retransmission:** An ACK was not received before the retransmission timer expired.
- **Duplicate ACK:** May indicate missing or out-of-order segments.
- **Zero Window:** The receiver's buffer is full and it tells the sender to pause transmission; this can indicate application-level latency.

#### Security Analysis
- **Possible scanning:** High volumes of SYN packets without a completed handshake, SYN/SYN-ACK/RST patterns, or unusual Xmas/Null flags.
- **TLS decryption:** Wireshark can decrypt supported TLS sessions when supplied with matching session secrets, such as those recorded through `SSLKEYLOGFILE` by supported browser setups.

### 3. Interview Q&A

**Q1. What is Wireshark?**  
Wireshark is an open-source packet analyzer used to capture and inspect network traffic.

**Q2. What is the difference between capture and display filters?**  
Capture filters decide which packets are captured. Display filters hide packets from the current view without deleting them from the capture.

**Q3. What is a dissector?**  
A protocol-specific component that interprets raw packet bytes and displays protocol fields in a readable format.

**Q4. Explain the TCP three-way handshake.**  
The client sends SYN, the server replies with SYN-ACK, and the client responds with ACK.

**Q5. What can TCP retransmissions indicate?**  
They occur when an acknowledgment is not received before the retransmission timer expires; packet loss is one possible cause.

**Q6. What does TCP Zero Window mean?**  
The receiving side reports that its buffer is full and asks the sender to pause transmission.

**Q7. How can Wireshark help identify scanning?**  
By revealing patterns such as large numbers of SYN packets without completed connections and unusual TCP flag combinations.

**Q8. Can Wireshark decrypt HTTPS/TLS traffic?**  
It can decrypt supported sessions when the matching TLS session secrets are available.

### 4. SOC Analyst Mindset

When investigating suspicious network traffic:

1. Identify the source and destination IP addresses.
2. Check the protocol and port.
3. Apply suitable display filters to narrow the investigation.
4. Follow the stream to understand the conversation.
5. Inspect TCP flags and handshake completion for possible scanning.
6. Review retransmissions, duplicate ACKs, and zero-window indicators when investigating network or application performance.
7. Remember that encrypted TLS payloads generally require matching session secrets for decryption.

**Important:** A suspicious packet pattern is an indicator to investigate, not proof of malicious activity by itself.

### 5. Final Memory Map

- **Capture:** Promiscuous Mode, Monitor Mode, libpcap, Npcap.
- **Understand packets:** Packet List → Packet Details → Packet Bytes.
- **Filter:** Capture = BPF; Display = Wireshark syntax.
- **Investigate conversations:** Follow Stream; Decode As.
- **TCP:** SYN → SYN-ACK → ACK.
- **Performance:** Retransmission, Duplicate ACK, Zero Window.
- **Security:** Scan patterns, Xmas/Null flags, TLS session-key-based decryption.

### Class 34 Recall Checklist

- [ ] Explain capture filters vs. display filters.
- [ ] Recall the important display-filter expressions.
- [ ] Explain the TCP three-way handshake.
- [ ] Differentiate retransmission, duplicate ACK, and zero window.
- [ ] Describe scanning indicators and TLS decryption requirements.

