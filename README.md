# Task 5 — Wireshark Capture & Analysis

**Author:** Likhith Bharadwaj Reddy  
**Date:** 29-09-2025  

---

## Objective  
Capture live network traffic using Wireshark, identify key protocols, and analyze selected packets.

---

## Deliverables  
- `capture/task5_capture_2025-09-29.pcapng` — packet capture file  
- `report.md` — short analysis report with protocols, endpoints, and findings  
- `commands.md` — Wireshark filters and analysis commands used  

---

## How to Use This Repo  

1. Open `capture/task5_capture_2025-09-29.pcapng` in **Wireshark**.  
2. Read `report.md` for the analysis (protocols observed, notable packets, conclusions, recommendations).  
3. Check `commands.md` for Wireshark filters and relevant commands (e.g., `dns`, `tcp.port==443`, `icmp`).  

---

## Notes & Privacy  

- The `.pcapng` file includes IP addresses and captured traffic.  
  - Local host: **192.168.1.10**  
  - Gateway/DNS server: **192.168.1.1**  
  - Remote server: **93.184.216.34**  
- Redact or anonymize IPs/domains before sharing publicly.  
- HTTPS/TLS traffic remains encrypted — decryption requires setting up `SSLKEYLOGFILE` or session keys.  
- Capture duration: ~60 seconds (29-09-2025, 11:00–11:01 IST).  

---
