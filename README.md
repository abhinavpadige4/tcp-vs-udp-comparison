# TCP vs UDP — A Clear Technical Comparison

A concise, interview-ready reference on the differences between the two dominant
transport-layer protocols of the Internet.

## What's in this repo

| File | Purpose |
|------|---------|
| [`tcp_udp_comparison.md`](./tcp_udp_comparison.md) | The full comparison document (main deliverable). |
| [`outline.md`](./outline.md) | Section-by-section outline used to structure the answer. |
| [`extracted_points.json`](./extracted_points.json) | Structured key points extracted from each source. |
| [`validation_report.txt`](./validation_report.txt) | Checklist confirming every requirement is satisfied. |

## TL;DR

- **TCP** = connection-oriented, reliable, ordered, slower, larger header (20 B).
  Use it when correctness matters: HTTP/HTTPS, SSH, email, file transfer.
- **UDP** = connectionless, unreliable, unordered, faster, smaller header (8 B).
  Use it when speed matters more than perfect delivery: DNS, VoIP, video
  streaming, gaming, QUIC/HTTP3.

## Quick comparison table

| Property | TCP | UDP |
|----------|-----|-----|
| Connection | Connection-oriented (3-way handshake) | Connectionless |
| Reliability | Reliable (ACKs + retransmission) | Best-effort, no guarantee |
| Ordering | Guaranteed in-order delivery | No ordering guarantee |
| Flow control | Yes (sliding window) | No |
| Congestion control | Yes (Reno, CUBIC, BBR, …) | No |
| Header size | 20 bytes (up to 60 with options) | 8 bytes (fixed) |
| Speed | Slower (overhead) | Faster (minimal overhead) |
| Error handling | End-to-end checksum + retransmit | Checksum only, no recovery |
| Typical uses | HTTP, HTTPS, SSH, SMTP, FTP, IMAP | DNS, VoIP, video streaming, gaming, NTP, QUIC |

## Sources referenced

1. Avast — *TCP vs UDP: Differences Between TCP & UDP Protocols*
   <https://www.avast.com/c-tcp-vs-udp-difference>
2. AVG — *What Is the Difference Between TCP and UDP?*
   <https://www.avg.com/en/signal/tcp-vs-udp>
3. IPCisco — *TCP vs UDP | 10 Key Differences Explained with Table & Examples*
   <https://ipcisco.com/lesson/tcp-versus-udp>
4. NetworkLessons — *Introduction to TCP and UDP*
   <https://networklessons.com/network-fundamentals/introduction-to-tcp-and-udp>
5. GeeksforGeeks — *Differences Between TCP and UDP*
   <https://www.geeksforgeeks.org/computer-networks/differences-between-tcp-and-udp>

See [`tcp_udp_comparison.md`](./tcp_udp_comparison.md) for the full write-up
with inline citations.
