# Findings: Tor Browser Network Traffic Analysis

## 1. Capture Overview

The analyzed Wireshark capture, `tor_baseline.pcapng`, contained 513 packets, approximately 249 kB of traffic, over 32.93 seconds.

## 2. Protocol and Conversation Analysis

The Conversations window displayed IPv4, IPv6, TCP and UDP traffic. The capture included multiple network endpoints and TCP conversations involving ports 443 and 8080.

This demonstrates that the selected network interface captured traffic using multiple network and transport-layer protocols.

## 3. TLS Handshake Analysis

**Display filter:** `tls.handshake.type == 1`

The filtered packet list showed five Client Hello packets in the displayed results. The visible SNI values included:

- `www.oiqhaff3.com`
- `nel.cloudflare.com`
- `win-extension.femetrics.grammarly.io`
- `ab.chatgpt.com`

These values are observations from the displayed capture. They do not establish which application generated each connection or whether the connections used Tor.

## 4. TCP Connection Analysis

The packet list contained TCP connection establishment packets, acknowledgments, retransmissions and connection termination packets.

The TCP handshake involves SYN, SYN-ACK and ACK packets. Retransmissions indicate that TCP attempted to resend segments; the screenshots alone do not establish why those retransmissions occurred.

## 5. Encrypted Traffic

The capture contained TLS 1.2 and TLS 1.3 traffic, including Application Data packets. The displayed packet summaries did not expose the plaintext contents of these encrypted application records.

Some TLS handshakes exposed SNI hostname metadata. The screenshots do not establish whether Encrypted Client Hello (ECH) was used for any particular connection.

## 6. Limitations

- The capture may contain traffic from multiple applications and background services.
- The presence of a hostname in SNI does not prove that a browser connected directly to that website.
- The capture does not independently prove that Tor carried every observed connection.
- The available evidence does not establish whether a DNS leak occurred.
- A packet capture cannot, by itself, establish the effectiveness of a browser's anonymity protections.

## 7. Conclusion

The project demonstrated how Wireshark can be used to inspect packet captures, analyze network conversations, identify TLS handshake metadata and examine TCP connection behavior.

The results illustrate that encrypted web communication can protect application payloads while some connection metadata remains observable. Correct attribution of traffic requires a controlled experimental setup and additional evidence beyond packet filtering alone.
