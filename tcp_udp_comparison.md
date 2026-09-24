# TCP vs UDP — A Clear Technical Comparison

> **One-line answer.** TCP is a *connection-oriented, reliable, ordered*
> transport protocol that trades speed for correctness; UDP is a
> *connectionless, best-effort* protocol that trades reliability for speed and
> low overhead.

Both protocols live at **Layer 4 (Transport Layer)** of the OSI model and sit
on top of IP. They share the same job — moving bytes between two endpoints —
but they make very different design trade-offs.

---

## 1. Connection Model

- **TCP is connection-oriented.** Before any data flows, the two endpoints
  establish a connection using a **3-way handshake** (SYN → SYN-ACK → ACK) and
  tear it down with a 4-way close (FIN/ACK exchange). Every TCP segment is
  associated with that connection.
- **UDP is connectionless.** There is no handshake and no session state. A
  sender simply sends a datagram to a destination IP + port; the receiver has
  no obligation to reply.

> *Sources: [Avast](https://www.avast.com/c-tcp-vs-udp-difference),
> [NetworkLessons](https://networklessons.com/network-fundamentals/introduction-to-tcp-and-udp),
> [IPCisco](https://ipcisco.com/lesson/tcp-versus-udp).*

## 2. Reliability

- **TCP is reliable.** Every segment is acknowledged (ACK) by the receiver.
  If an ACK is not received within the retransmission timeout, the sender
  retransmits the segment. Lost, duplicated, or corrupted segments are
  transparently recovered.
- **UDP is unreliable (best-effort).** There are no ACKs and no retransmissions.
  If a datagram is dropped, it is simply gone. The application is responsible
  for any recovery logic it needs.

> *Sources: [AVG](https://www.avg.com/en/signal/tcp-vs-udp),
> [GeeksforGeeks](https://www.geeksforgeeks.org/computer-networks/differences-between-tcp-and-udp).*

## 3. Ordering

- **TCP guarantees in-order delivery.** Segments carry sequence numbers; the
  receiver reassembles them in order before handing data to the application.
- **UDP does not guarantee ordering.** Two datagrams sent back-to-back may
  arrive out of order, or one may be dropped entirely.

> *Source: [IPCisco](https://ipcisco.com/lesson/tcp-versus-udp).*

## 4. Flow Control

- **TCP has flow control** via a **sliding window** (the receiver advertises
  how much buffer space it has in the `Window` field of the TCP header). The
  sender throttles itself so it does not overwhelm a slow receiver.
- **UDP has no flow control.** The sender can blast datagrams as fast as it
  wants; if the receiver cannot keep up, packets are dropped.

> *Source: [NetworkLessons](https://networklessons.com/network-fundamentals/introduction-to-tcp-and-udp).*

## 5. Congestion Control

- **TCP has congestion control.** Algorithms such as **Reno, CUBIC, and BBR**
  dynamically reduce the sending rate when the network shows signs of
  congestion (packet loss, RTT increase), protecting the wider Internet.
- **UDP has no congestion control.** This is why UDP-based applications
  (video streaming, gaming) must implement their own rate adaptation, or
  rely on a higher layer such as **QUIC** (which runs over UDP but adds
  congestion control on top).

> *Sources: [AVG](https://www.avg.com/en/signal/tcp-vs-udp),
> [GeeksforGeeks](https://www.geeksforgeeks.org/computer-networks/differences-between-tcp-and-udp).*

## 6. Header Size

- **TCP header: 20 bytes minimum**, up to 60 bytes with options.
- **UDP header: 8 bytes, fixed.**

UDP's smaller header means less per-packet overhead — a big deal for
small, frequent messages (e.g., DNS queries).

> *Sources: [Avast](https://www.avast.com/c-tcp-vs-udp-difference),
> [IPCisco](https://ipcisco.com/lesson/tcp-versus-udp).*

## 7. Speed & Overhead

- **TCP is slower** because of the handshake, ACKs, retransmissions, and
  congestion/flow-control bookkeeping.
- **UDP is faster** — no handshake, no ACKs, minimal header. This makes it
  ideal for real-time media where a slightly late frame is worse than a
  dropped frame.

> *Source: [AVG](https://www.avg.com/en/signal/tcp-vs-udp).*

## 8. Error Handling

- **TCP** performs end-to-end error detection (checksum) *and* recovery
  (retransmission).
- **UDP** performs only a checksum; if the checksum fails, the datagram is
  silently discarded.

## 9. Typical Use Cases

### TCP — when correctness matters

- **HTTP / HTTPS** — web browsing
- **SSH / Telnet** — remote shell
- **SMTP / IMAP / POP3** — email
- **FTP / SFTP** — file transfer
- **Database protocols** (MySQL, PostgreSQL)
- **Any API that must not lose data**

### UDP — when speed matters

- **DNS** — name resolution (small, frequent queries)
- **VoIP / SIP** — voice calls (Skype, Zoom audio)
- **Video streaming** — YouTube, Twitch, WebRTC
- **Online gaming** — real-time multiplayer
- **NTP** — time synchronization
- **DHCP** — address assignment
- **QUIC / HTTP/3** — modern transport that runs *over* UDP

> *Sources: [Avast](https://www.avast.com/c-tcp-vs-udp-difference),
> [IPCisco](https://ipcisco.com/lesson/tcp-versus-udp),
> [NetworkLessons](https://networklessons.com/network-fundamentals/introduction-to-tcp-and-udp).*

---

## Side-by-side summary

| Property | TCP | UDP |
|---|---|---|
| Full name | Transmission Control Protocol | User Datagram Protocol |
| Connection | Connection-oriented (3-way handshake) | Connectionless |
| Reliability | Reliable (ACKs + retransmission) | Best-effort, no guarantee |
| Ordering | Guaranteed | Not guaranteed |
| Flow control | Yes (sliding window) | No |
| Congestion control | Yes (Reno, CUBIC, BBR) | No |
| Header size | 20 B (min) / 60 B (max) | 8 B (fixed) |
| Speed | Slower | Faster |
| Error handling | Checksum + retransmit | Checksum only |
| Duplex | Full-duplex | Full-duplex |
| Best for | Correctness, integrity | Speed, low latency |
| Examples | HTTP, HTTPS, SSH, SMTP, FTP | DNS, VoIP, video, gaming, NTP, QUIC |

---

## When to pick which?

- **Pick TCP** when you cannot afford to lose or reorder data: web pages,
  file uploads, database writes, authentication.
- **Pick UDP** when a stale packet is worse than a missing one: live video,
  voice, gaming, or when you need to build your own reliability on top
  (as QUIC does).

---

## References

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
