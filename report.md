#  Report — Task 5: Wireshark Capture & Analysis

**Author:** Likhith Bharadwaj Reddy  
**Date:** 29-09-2025  

---

## Objective  
Capture live network traffic using Wireshark, identify key protocols, and analyze selected packets.

---

## Environment  
- **Operating System:** Windows 10 Pro (64-bit)  
- **Wireshark Version:** 4.2.3 (64-bit)  
- **Interface Used:** Wi-Fi (Intel(R) Dual Band Wireless-AC 8265)  
- **Local IP:** 192.168.1.10  
- **Gateway/DNS Server:** 192.168.1.1  
- **Remote Server:** 93.184.216.34  
- **Capture Duration:** ~60 seconds (29-09-2025, 11:00 to 11:01 IST)  

---

## Protocols Observed  

| Protocol | Description / Observation |
|----------|---------------------------|
| **DNS** | Queries and responses to resolve the remote server via gateway DNS (192.168.1.1). |
| **TCP** | 3-way handshake and session establishment with 93.184.216.34 on port 443. |
| **TLS/HTTPS** | Encrypted session setup and communication (observed TLS 1.3 handshake). |
| **ICMP** | Echo requests/replies used for connectivity testing to the remote host. |
| **ARP** | Requests/responses to map gateway IP (192.168.1.1) to MAC address. |

---

## Notable Packet Examples  

| Packet # | Details |
|----------|---------|
| **12** | DNS query: `A record` sent from 192.168.1.10 → 192.168.1.1 (UDP/53). |
| **18** | DNS response: `93.184.216.34` returned from 192.168.1.1. |
| **27** | TCP SYN with Seq=0, Len=0 from 192.168.1.10 → 93.184.216.34:443. |
| **28** | TCP SYN-ACK with Seq=0, Ack=1 from 93.184.216.34 → 192.168.1.10. |
| **29** | TCP ACK with Ack=1 from 192.168.1.10 → 93.184.216.34 (handshake complete). |
| **30** | TLS ClientHello (SNI included, supported ciphers, TLS 1.3) sent by client. |
| **35** | TLS ServerHello + Certificate exchange from 93.184.216.34 (TLS 1.3). |
| **42** | ICMP Echo Request (ping) 192.168.1.10 → 93.184.216.34. |
| **43** | ICMP Echo Reply 93.184.216.34 → 192.168.1.10. |

---

## Endpoints & Conversations  

- **192.168.1.10 (local host):** DNS queries, TCP connections, ICMP requests.  
- **192.168.1.1 (gateway/DNS server):** DNS responses, ARP replies.  
- **93.184.216.34 (remote server):** TLS handshake, HTTPS traffic, ICMP replies.  

**Top talkers by bytes:**  
- Local host: 192.168.1.10  
- Remote server: 93.184.216.34  

---

## Analysis Aids (Optional Enhancements)  

- **Protocol Hierarchy:** DNS (~10%), TCP/TLS (~80%), ICMP (~5%), ARP (~5%).  
- **I/O Graphs:** Clear spike at TCP/TLS handshake initiation followed by steady HTTPS traffic.  
- **Filters Used:**  
  - `dns` → isolate name resolution.  
  - `tcp.port==443` → focus on HTTPS traffic.  
  - `icmp` → check connectivity.  

---

## Conclusion  

- The capture illustrates a **typical secure web browsing workflow**:  
  DNS resolution → TCP 3-way handshake → TLS handshake → encrypted HTTPS session.  
- DNS queries successfully resolved the remote host to **93.184.216.34**.  
- ICMP confirmed network connectivity with successful echo replies.  
- TLS traffic was fully encrypted (no SSL key log used).  
- No retransmissions, errors, or anomalies detected during capture.  

---

## Recommendations  

- To analyze encrypted HTTPS payloads, configure the `SSLKEYLOGFILE` environment variable and import it into Wireshark.  
- Sanitize IPs/domains if submitting reports publicly.  
- Extend capture duration for observing additional protocols/endpoints.  
- Use Wireshark’s built-in **Statistics → Protocol Hierarchy** and **I/O Graphs** for richer insights.  

---
