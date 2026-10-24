# Tor Browser Network Traffic Analysis Using Wireshark

## 1. Objective

The objective of this project was to capture and analyze network traffic during a Tor Browser testing session using Wireshark, examine the protocols and connection patterns, and understand what network-level information remains observable when encrypted web traffic is used.

## 2. Tools Used

- Wireshark — packet capture and protocol analysis
- Tor Browser — controlled browsing environment
- Windows — host operating system

## 3. Methodology

1. Selected the active Wi-Fi network interface in Wireshark.
2. Captured network packets during the testing session.
3. Saved the capture as `tor_baseline.pcapng`.
4. Examined conversations to identify communicating endpoints, protocols, ports, packet counts and byte volumes.
5. Applied display filters to inspect TCP connections, TLS handshakes, DNS traffic and retransmissions.
6. Examined packet metadata to understand the visibility and limitations of encrypted network traffic.

## 4. Observations and Findings

### 4.1 Packet Capture Statistics

The analyzed capture contained 513 packets, approximately 249 kB of traffic, over a duration of approximately 32.93 seconds.

### 4.2 Protocol Analysis

The Conversations window displayed IPv4, IPv6, TCP and UDP traffic. TCP conversations included connections involving ports 443 and 8080.

### 4.3 TLS Handshake Analysis

The filter `tls.handshake.type == 1` identified Client Hello messages using TLS 1.2 and TLS 1.3. The packet list displayed Server Name Indication (SNI) values for several hostnames.

This demonstrates that some hostname metadata can be visible during TLS handshakes, depending on the connection and protocol configuration.

### 4.4 TCP Connection Behavior

The capture contained TCP connection establishment packets, acknowledgments, retransmissions and connection termination packets. These observations illustrate the mechanisms TCP uses to establish connections, acknowledge data and manage communication.

Retransmissions were observed, but the available screenshots do not establish their underlying cause.

### 4.5 Encrypted Traffic

TLS Application Data packets were present. Their encrypted payloads could not be interpreted as ordinary webpage content from the packet list alone.

Encryption protects application data, but it does not necessarily conceal every aspect of network communication.

## 5. Key Findings

- Wireshark can capture and classify network traffic by protocol, endpoint and port.
- TLS handshake metadata can reveal information such as SNI when it is available in the capture.
- TCP connection behavior can be studied through flags, sequence numbers, acknowledgments and retransmissions.
- Encrypted application payloads are not directly readable as ordinary plaintext without appropriate decryption material and conditions.
- A packet capture from a computer may include traffic from multiple applications and background services.

## 6. Limitations

The available screenshots do not independently establish which application generated every connection. The presence of a hostname in a TLS Client Hello does not, by itself, prove that the corresponding connection bypassed Tor or that the hostname was visited directly by a particular browser.

The analysis also does not establish the absence of DNS leaks, the effectiveness of anonymity protections, or the origin of every observed packet. These conclusions would require additional controlled evidence.

## 7. Conclusion

This project demonstrated the practical use of Wireshark for network traffic capture, protocol filtering, conversation analysis and TLS/TCP inspection. The observations highlighted the difference between visible network metadata and encrypted application content.

The project also demonstrated the importance of interpreting packet captures carefully: traffic observed on a network interface cannot automatically be attributed to a single application. Establishing whether a connection belongs to Tor Browser requires correlating the capture with a controlled test and appropriate connection-level evidence.

Overall, the project provided hands-on experience with packet analysis, encrypted network communication, TCP behavior and the limitations of passive network monitoring.
