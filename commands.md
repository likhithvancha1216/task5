# Wireshark Filters & Analysis Commands — Task 5

## Display Filters Used
- `dns` → Show DNS queries and responses  
- `tcp` → Show TCP packets  
- `tcp.port == 443` → Focus on HTTPS/TLS traffic  
- `tls` → Show TLS handshake and encrypted messages  
- `icmp` → Display ping requests and replies  
- `arp` → Show ARP traffic  

## Useful Wireshark Features
- **Follow TCP Stream** → Inspect TCP session data (though TLS will be encrypted).  
- **Statistics → Protocol Hierarchy** → View distribution of DNS, TCP, TLS, ICMP, ARP.  
- **Statistics → Conversations** → Identify active conversations (local ↔ gateway, local ↔ remote).  
- **Statistics → Endpoints** → See total traffic per endpoint.  

## Command-Line (tshark)
```bash
# Extract DNS traffic
tshark -r Wireshark\ Packet\ Capture\ Analysis.pcapng -Y "dns"

# Extract TCP traffic
tshark -r Wireshark\ Packet\ Capture\ Analysis.pcapng -Y "tcp"

# Extract TLS handshakes
tshark -r Wireshark\ Packet\ Capture\ Analysis.pcapng -Y "tls"

# Extract ICMP traffic
tshark -r Wireshark\ Packet\ Capture\ Analysis.pcapng -Y "icmp"

# Extract ARP traffic
tshark -r Wireshark\ Packet\ Capture\ Analysis.pcapng -Y "arp"
