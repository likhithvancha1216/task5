# Short Report — Task 5: Wireshark Capture & Analysis

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
| **DNS** | Queries and responses between 192.168.1.10 and 192.168.1.1. |
| **TCP** | TCP connection initiation with 93.184.216.34. |
| **TLS/HTTPS** | Encrypted session handshake with remote server. |
| **ICMP** | Echo requests and replies with 93.184.216.34. |
| **ARP** | ARP request from local host to gateway. |

---

## Notable Packet Examples  

| Packet # | Details |
|----------|---------|
| **1** | DNS query from 192.168.1.10 → 192.168.1.1 (UDP/53). |
| **2** | DNS response from 192.168.1.1 → 192.168.1.10. |
| **3** | TCP connection attempt from 192.168.1.10 → 93.184.216.34. |
| **4** | TLS ClientHello from 192.168.1.10 → 93.184.216.34. |
| **5** | TLS ServerHello from 93.184.216.34 → 192.168.1.10. |
| **6** | TLS Encrypted Handshake Message exchange. |
| **8** | ICMP Echo Request/Reply between 192.168.1.10 ↔ 93.184.216.34. |
| **10** | ARP query from 192.168.1.1. |

---

## Endpoints & Conversations  

- **192.168.1.10 ↔ 192.168.1.1**: DNS queries/responses and ARP.  
- **192.168.1.10 ↔ 93.184.216.34**: TCP + TLS encrypted session.  
- **192.168.1.10 ↔ 93.184.216.34**: ICMP ping tests.  

**Top talkers by bytes:**  
- Local host: 192.168.1.10  
- Remote server: 93.184.216.34  

---

## Capture Screenshot  

![Wireshark Capture](Wireshark%20Packet%20Capture%20Analysis.png)

---

## Conclusion  

- The capture shows a normal secure browsing workflow: DNS resolution → TCP handshake → TLS handshake → encrypted data.  
- DNS queries resolved the remote server correctly.  
- ICMP traffic confirmed host connectivity.  
- TLS traffic remained encrypted, as expected.  
- No packet loss or retransmissions observed.  

---

## Recommendations  

- Use `SSLKEYLOGFILE` to decrypt TLS payloads if deeper inspection is needed.  
- Redact sensitive IPs/domains before public sharing.  
- Longer captures may reveal additional protocols.  
