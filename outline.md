# TCP vs UDP — Outline

## 1. Connection Model
- TCP: connection-oriented, 3-way handshake (SYN / SYN-ACK / ACK), 4-way close.
- UDP: connectionless, no handshake, no session state.

## 2. Reliability
- TCP: reliable — ACKs, retransmission on timeout, duplicate suppression.
- UDP: best-effort — no ACKs, no retransmission.

## 3. Ordering
- TCP: sequence numbers guarantee in-order delivery.
- UDP: no ordering guarantee.

## 4. Flow Control
- TCP: sliding window, receiver-advertised window size.
- UDP: none.

## 5. Congestion Control
- TCP: Reno, CUBIC, BBR — adapts rate to network conditions.
- UDP: none (application or QUIC must handle it).

## 6. Header Size
- TCP: 20 bytes minimum, up to 60 with options.
- UDP: 8 bytes, fixed.

## 7. Speed & Overhead
- TCP: slower due to handshake, ACKs, retransmissions.
- UDP: faster, minimal overhead.

## 8. Error Handling
- TCP: checksum + retransmission.
- UDP: checksum only, silent discard on failure.

## 9. Use Cases
- TCP: HTTP/HTTPS, SSH, SMTP, FTP, databases.
- UDP: DNS, VoIP, video streaming, gaming, NTP, DHCP, QUIC/HTTP3.

## 10. Decision Guide
- Correctness matters → TCP.
- Speed / low latency matters → UDP.
