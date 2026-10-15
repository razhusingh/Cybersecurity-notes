
# SOC Analyst L1 — Class 34
# Network Traffic Analysis with Wireshark

## 1. Network Traffic

### 1.1 What Is Network Traffic?

Network traffic is all the digital data moving across a network at a particular time.

Examples:
- Loading a website.
- Sending an email.
- Streaming a video.

The operating system divides transmitted data into small pieces called **packets**. These packets travel through network protocol layers such as the OSI or TCP/IP model.

### 1.2 Encapsulation

Encapsulation is the process in which each network layer adds its own control information to the data as it moves down the protocol stack.

A packet contains two important parts:

**Header**
- MAC addresses.
- IP addresses.
- Port numbers.
- Flags.
- Sequence numbers.
- Checksums.

**Payload**
- The actual data being transferred.
- HTML text.
- Image data.
- Encrypted data.

**Easy explanation:** The header contains addressing and control information, while the payload contains the actual data.

---

## 2. Wireshark Basics and Architecture

### 2.1 What Is Wireshark?

Wireshark is an open-source network packet analyzer, also called a packet sniffer.

It allows analysts to:
- Capture network traffic in real time.
- Inspect individual packets.
- Browse network conversations.
- Analyze previously captured traffic files.

Common capture file formats:
- `.pcap`
- `.pcapng`

### 2.2 Wireshark Interface

The interface diagram contains three main areas:

**Packet List**
- Displays captured packets in rows.
- Shows Time, Source, Destination, Protocol, Length and Info.

**Packet Details**
- Displays the selected packet's protocol fields and structure.

**Packet Bytes**
- Displays the packet's raw hexadecimal bytes and corresponding data representation.

**Remember:**
- Packet List = View traffic.
- Packet Details = Understand packet structure.
- Packet Bytes = Inspect underlying data.

---

## 3. How Wireshark Captures Packets

### 3.1 Promiscuous Mode

Normally, a Network Interface Card (NIC) passes frames addressed to its own MAC address to the operating system.

Wireshark can enable **Promiscuous Mode**, allowing the NIC to capture frames it can observe on the physical network medium, including frames addressed to other devices.

For Wi-Fi, the class also mentions **Monitor Mode**.

### 3.2 Capture Core Libraries

Wireshark uses low-level packet capture libraries to communicate with the network card and its driver.

| Library | Platform |
|---|---|
| libpcap | Unix/Linux |
| Npcap | Windows |

The class identifies Npcap as the successor to WinPcap.

### 3.3 Dissectors

Dissectors are built-in modules that understand particular network protocols.

Examples:
- DNS
- HTTP
- TCP
- ARP

**How they work:**
1. Wireshark captures raw packet bytes.
2. The relevant dissector examines the bytes.
3. It interprets the protocol fields.
4. Wireshark displays the information in a human-readable format.

**Easy explanation:** Dissectors translate raw packet data into readable protocol information.

---

## 4. Capture Filters vs Display Filters

Wireshark provides two types of filters.

### 4.1 Capture Filters

Capture filters are applied before or during packet capture.

They use **Berkeley Packet Filter (BPF)** syntax.

**Purpose:**
- Discard unwanted packets during capture.
- Reduce the amount of captured data.
- Reduce processing and storage requirements.

Example:

    host 192.168.1.1 and port 80

This selects traffic involving the specified host and port.

### 4.2 Display Filters

Display filters are applied after packets have been captured.

They use Wireshark's display-filter syntax.

**Purpose:**
- Hide irrelevant packets from the displayed results.
- Keep the captured data available in memory.

Example:

    ip.addr == 192.168.1.1 && tcp.port == 80

This displays packets matching the specified IP address and TCP port.

### 4.3 Key Differences

| Feature | Capture Filter | Display Filter |
|---|---|---|
| When applied | Before/during capture | After capture |
| Syntax | BPF | Wireshark display-filter syntax |
| Purpose | Discards unwanted packets from the capture | Hides irrelevant packets from the view |
| CPU load | Generally lower | Can be higher because packets are dissected and evaluated |

**Remember:**
- Capture Filter = Decide what to capture.
- Display Filter = Decide what to display.

---

## 5. Wireshark Display Filter Cheat Sheet

### 5.1 Filter by IP Address

**Source IP:**

    ip.src == 10.0.0.5

Displays packets whose source IP is `10.0.0.5`.

**Destination IP:**

    ip.dst == 10.0.0.1

Displays packets whose destination IP is `10.0.0.1`.

### 5.2 Filter by Protocol

    dns
    http
    arp
    icmp
    tls

These filters display packets identified as the corresponding protocols.

### 5.3 Filter by Port

**TCP port 443:**

    tcp.port == 443

**UDP port 53:**

    udp.port == 53

### 5.4 Boolean Operators

Example:

    ip.addr == 192.168.1.1 && !tcp.port == 80

- `&&` means AND.
- `!` means NOT.

The expression combines an IP address condition with an exclusion condition for TCP port 80.

### 5.5 Filter by HTTP Request Method

    http.request.method == "POST"

Displays HTTP requests whose method is POST.

### 5.6 Filter by DNS Query Name

    dns.qry.name contains "example"

Displays DNS queries whose query name contains `example`.

---

## 6. Follow Stream and Decode As

### 6.1 Follow Stream

Follow Stream reconstructs the conversation associated with a particular network connection.

**How to use it:**
1. Select a packet.
2. Right-click the packet.
3. Select Follow → TCP Stream.

The class also mentions following UDP and HTTP streams.

**What it does:**
- Isolates packets belonging to the selected conversation.
- Reconstructs the payload into sequential data.
- Helps analysts inspect communication between endpoints.

**Easy explanation:** Instead of inspecting packets separately, Follow Stream helps you understand the conversation they form.

### 6.2 Decode As

Sometimes traffic uses a non-standard port.

Example: HTTP traffic running on port `8080`.

Wireshark may not automatically interpret the traffic using the intended protocol.

**How to use Decode As:**
1. Right-click the relevant packet.
2. Select Decode As.
3. Manually assign the appropriate protocol.

**Purpose:** Tell Wireshark which protocol dissector to use for the selected traffic.

---

## 7. Standard TCP Three-Way Handshake

### 7.1 What Is a TCP Handshake?

A TCP three-way handshake establishes a connection between a client and a server.

It synchronizes their sequence numbers before normal data transfer.

### Step 1: SYN

**Client → Server**

The client initiates the connection by sending a SYN packet and providing its initial sequence number.

### Step 2: SYN-ACK

**Server → Client**

The server acknowledges the client's request and sends its own SYN, providing the server's initial sequence number.

### Step 3: ACK

**Client → Server**

The client acknowledges the server's SYN.

After the handshake succeeds, the TCP connection becomes **ESTABLISHED**.

### 7.2 Handshake Diagram

    Client                         Server
       |                              |
       | -------- SYN --------------> |
       |                              |
       | <------ SYN-ACK ------------ |
       |                              |
       | -------- ACK --------------> |
       |                              |
       |                       ESTABLISHED

### 7.3 Sequence Number Example

| Step | Direction | Flags | Sequence/Acknowledgment |
|---|---|---|---|
| 1 | Client → Server | SYN | Seq = 0 |
| 2 | Server → Client | SYN-ACK | Ack = 1, Seq = 0 |
| 3 | Client → Server | ACK | Seq = 1, Ack = 1 |

These values illustrate the simplified example shown in the class.

**Remember:** SYN → SYN-ACK → ACK.

---

## 8. Identifying Network Performance Issues

Wireshark provides TCP Expert Info flags that help identify network and communication problems.

### 8.1 TCP Retransmissions

A retransmission occurs when TCP sends data again because the expected acknowledgment was not received before the retransmission timer expired.

**Possible indication:** Packets may have been lost or delayed.

**Investigation:** Examine retransmissions when investigating unreliable or slow connections.

### 8.2 TCP Duplicate ACK

The receiver repeatedly acknowledges the same sequence position when it receives out-of-order segments or detects missing data.

Possible indications:
- A missing segment.
- Out-of-order packet arrival.

Repeated acknowledgments help TCP identify missing data and can trigger retransmission.

### 8.3 TCP Zero Window

The receiver's buffer is full.

The receiver advertises a zero window, telling the sender to pause sending additional data.

The receiving application may not be processing incoming data quickly enough, contributing to application-level latency.

### 8.4 Quick Comparison

| TCP Expert Info | Meaning | What to Investigate |
|---|---|---|
| Retransmission | Data sent again because an acknowledgment was not received in time | Possible packet loss or delay |
| Duplicate ACK | Repeated acknowledgment associated with missing or out-of-order segments | Packet ordering and missing data |
| Zero Window | Receiver cannot currently accept more data | Receiver buffer and application responsiveness |

---

## 9. Security Analysis: Detecting Network Scanning

### 9.1 Recognizing Port Scanning

Attackers may use tools such as Nmap to discover open ports and services.

Wireshark can help identify scanning patterns.

**Indicators mentioned in the class:**
- A high volume of SYN packets.
- Connections that do not complete the TCP three-way handshake.
- SYN packets followed by SYN-ACK and RST patterns.
- Unusual TCP flag combinations, including Xmas and Null scans.

### 9.2 Why Is This Important?

A normal TCP connection generally completes the three-way handshake.

During reconnaissance, an attacker may probe many ports without establishing normal connections.

### 9.3 SOC Investigation

1. Identify the source IP.
2. Examine the destination IP.
3. Look for a high volume of SYN packets.
4. Check whether handshakes complete.
5. Examine unusual TCP flag combinations.

**Remember:** Many connection attempts without normal handshake completion can indicate scanning activity.

---

## 10. Decrypting HTTPS/TLS Traffic

### 10.1 Why Is TLS Decryption Needed?

Modern web traffic often uses TLS encryption.

Encrypted traffic can prevent an analyst from directly reading the application payload in a packet capture.

### 10.2 SSLKEYLOGFILE

The class explains that Wireshark can decrypt supported TLS sessions when provided with an `SSLKEYLOGFILE` exported by a browser such as Chrome or Firefox.

### 10.3 Basic Process

1. Configure the browser to export TLS session secrets to an `SSLKEYLOGFILE`.
2. Capture the relevant network traffic.
3. Provide the key-log file to Wireshark's TLS decryption settings.
4. Wireshark uses matching session secrets to decrypt supported traffic.
5. Inspect the decrypted communication where available.

**Important:** The key-log file must contain session secrets corresponding to the captured TLS connections.

### 10.4 Why Is This Useful?

It allows analysts to inspect supported encrypted sessions when the necessary session secrets are available.

---

## 11. Final Quick Revision

### Network Traffic
- Network traffic = Data moving across a network.
- Packets = Small chunks of transmitted data.
- Encapsulation = Each protocol layer adds control information.
- Header = Addressing and control information.
- Payload = Actual transferred data.

### Wireshark
- Open-source network packet analyzer.
- Captures live traffic and analyzes `.pcap` and `.pcapng` files.
- Promiscuous Mode captures observable frames beyond those addressed to the NIC.
- libpcap = Unix/Linux.
- Npcap = Windows.
- Dissectors translate packet bytes into readable protocol fields.

### Filters
- Capture Filter = Before/during capture; BPF syntax.
- Display Filter = After capture; Wireshark syntax.
- Follow Stream = Reconstruct a conversation.
- Decode As = Manually assign a protocol dissector.

### TCP Handshake
SYN → SYN-ACK → ACK → ESTABLISHED

### Performance Issues
- Retransmission = Data sent again after an acknowledgment timeout.
- Duplicate ACK = Repeated acknowledgment associated with missing/out-of-order segments.
- Zero Window = Receiver buffer is full.

### Security Analysis
- Many SYN packets and incomplete handshakes may indicate scanning.
- Xmas/Null scans use unusual TCP flag combinations.
- TLS decryption may be possible when matching browser session secrets are available.
