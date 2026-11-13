# Securing a Multi-Site Enterprise Network (Cisco Packet Tracer)

**Module:** Network Security (COMP H1001) | **Academic project:** August 2026  
**Focus:** Network hardening, secure administration, IPsec VPN, access controls and validation

## Project overview

The Cisco Packet Tracer topology already connected **Dublin, London and Beijing** when I started. My task was to **secure the existing network without breaking working services**. I added a separate Cisco VPN router in Beijing because the existing wireless router did not support the required IOS IPsec commands; the original wireless router was then used as an access point.

## Technologies and concepts

Cisco Packet Tracer, Cisco IOS CLI, SSHv2, RADIUS/AAA, syslog, NTP, OSPF message-digest authentication, IKE/ISAKMP and IPsec, extended IPv4 ACLs, VLANs, 802.1Q trunks, port security, DHCP snooping, BPDU Guard, WPA2-Personal/AES, static NAT and PAT.

## What I implemented

1. **Device hardening:** Protected router/switch management, enabled SSH-only remote access, configured login controls and kept a local administrator fallback for RADIUS outages.
2. **Central authentication and monitoring:** Used a RADIUS server in London for Dublin/London technician SSH access, with central syslog and NTP for devices across the topology.
3. **Authenticated routing:** Secured the existing Dublin–London OSPF relationship with message-digest authentication supported by the simulator.
4. **Site-to-site IPsec VPN:** Configured the Dublin and Beijing routers for IKE phase 1 with AES-256 and pre-shared-key authentication, and IPsec phase 2 for protected company traffic. Verified tunnel negotiation and traffic counters.
5. **Traffic restrictions:** Applied extended ACLs to control which LANs and services could communicate, including separation of Dublin Sales and Purchasing, allowed services to London, and permitted Purchasing-to-Beijing traffic.
6. **Layer 2 security:** Implemented VLAN 10 (Sales), VLAN 20 (Purchasing), VLAN 999 for unused/native use, fixed trunks, port security, PortFast/BPDU Guard and DHCP snooping.
7. **Wireless and addressing:** Hardened the Beijing WLAN with WPA2/AES and additional device restrictions. Configured static NAT for London servers and PAT for London administrative clients.

## Validation and results

I tested allowed and blocked traffic throughout the project rather than making all changes before testing:

- Successful RADIUS-authenticated SSH administration from the London Admin LAN.
- OSPF neighbours returned to **FULL** following authentication setup.
- VPN verification reported **QM_IDLE/ACTIVE** and non-zero encrypt/decrypt counters.
- ACL tests showed permitted services and denied unauthorised LAN paths.
- The report documents working web-service access, NAT/PAT tests and Beijing-to-Dublin connectivity through the secured path.

## Challenges and limitations

- The original Beijing router lacked the required IPsec commands; I introduced a separate VPN-capable simulated router.
- Packet Tracer only supported older RSA/Diffie-Hellman options on the selected devices; these should **not** be copied as modern production recommendations.
- DHCP snooping Option 82 caused issues in the simulator, so Option 82 insertion was disabled while the main snooping controls remained enabled.
- This was an **academic simulation**, not a deployed corporate network. The original `.pkt` file was not supplied for this public package; the report is the evidence available here.

## My contribution

I secured the provided topology, made the justified Beijing topology change, applied router/switch/WLAN security settings and tested remote access, routing, VPN operation, filtering and network services. I recorded the configuration and validation in the coursework report.

## Evidence

- [Selected, sanitised pages from my network security report](evidence/sanitised-report-excerpts.pdf)
- [Packet Tracer topology](evidence/network-topology.png)
- [Site-to-site IPsec VPN verification](evidence/ipsec-vpn-verification.png)

The report uses **simulated/example IP addresses**. Actual administrative and VPN secrets are intentionally excluded; **do not publish an unreviewed `.pkt` file**, since it may store configuration secrets.
