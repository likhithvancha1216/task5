# Task 5 — Wireshark Filters & Analysis Commands

**Author:** Likhith Bharadwaj Reddy  
**Date:** 29-09-2025  

---

## Capture Setup  

- **Interface Used:** Wi-Fi (Intel(R) Dual Band Wireless-AC 8265)  
- **Duration:** ~60 seconds  
- **Saved File:** `capture/task5_capture_2025-09-29.pcapng`  

---

## Display Filters Used  

| Filter | Purpose / Analysis |
|--------|--------------------|
| `dns` | Isolate DNS queries/responses (verify resolution of remote server). |
| `tcp.port==443` | Show only HTTPS/TLS traffic (TCP handshake + TLS handshake). |
| `icmp` | Display ICMP Echo Request/Reply packets (connectivity check). |
| `arp` | Show ARP requests/replies (local-to-gateway MAC resolution). |
| `ip.addr==93.184.216.34` | Focus on traffic with the remote server. |
| `ip.addr==192.168.1.10` | Focus on local host traffic. |
| `ip.addr==192.168.1.1` | Focus on gateway/DNS server traffic. |

---

## Analysis Steps in Wireshark  

1. **DNS Resolution**  
   - Filter: `dns`  
   - Observed DNS query for remote server, response with IP `93.184.216.34`.  

2. **TCP 3-Way Handshake**  
   - Filter: `tcp.port==443`  
   - Verified SYN → SYN-ACK → ACK sequence between local host and remote server.  

3. **TLS Handshake**  
   - Filter: `tcp.port==443`  
   - Checked `ClientHello` (SNI, supported ciphers, TLS version) and `ServerHello` + Certificate.  

4. **ICMP Connectivity**  
   - Filter: `icmp`  
   - Verified Echo Request (local → remote) and Echo Reply (remote → local).  

5. **ARP Requests**  
   - Filter: `arp`  
   - Confirmed mapping of gateway IP `192.168.1.1` to MAC address.  

---

## Useful Wireshark Menu Options  

- **Statistics → Protocol Hierarchy** → Breakdown of protocols (DNS, TCP, TLS, ICMP, ARP).  
- **Statistics → Conversations** → List of IPs and traffic volume between local host, gateway, and remote server.  
- **Statistics → I/O Graphs** → Visualize traffic spikes (e.g., handshake initiation).  

---

## Optional Command-Line (tshark) Examples  

For automated analysis (if required):  

```bash
# List all DNS queries
tshark -r capture/task5_capture_2025-09-29.pcapng -Y "dns" -T fields -e dns.qry.name

# Show all TCP handshakes on port 443
tshark -r capture/task5_capture_2025-09-29.pcapng -Y "tcp.port==443" -T fields -e ip.src -e ip.dst -e tcp.flags

# Extract only ICMP packets
tshark -r capture/task5_capture_2025-09-29.pcapng -Y "icmp"

# Show ARP communications
tshark -r capture/task5_capture_2025-09-29.pcapng -Y "arp"
