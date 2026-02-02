# Day 1 – Networking Basics & Lab Wiring

## Objective
The objective of this lab was to understand how systems communicate
within a small enterprise-style network by designing, wiring,
configuring, and troubleshooting a virtual lab environment.

This lab focuses on how traffic flows between hosts, how IP addressing
and services are assigned, and how a firewall operates as the
central communication point.

---

## Lab Environment

### Tools Used
- VirtualBox
- pfSense Community Edition
- Ubuntu Server
- Kali Linux
- Windows 10

---

## Network Design

### Architecture Overview
- pfSense acts as the perimeter firewall and default gateway
- WAN interface connects to the Internet using VirtualBox NAT
- LAN interface connects to an isolated Internal Network (`soc_lan`)
- All client machines reside on the same LAN segment

A simple star topology was used, with pfSense positioned at the center
of all network communication.

---

## IP Addressing Strategy

| Device | Addressing Method |
|------|-------------------|
| pfSense (LAN) | Static – 192.168.10.1/24 |
| Ubuntu Server | DHCP |
| Windows 10 | DHCP |
| Kali Linux | DHCP |

Static addressing was applied to the firewall LAN interface to ensure a
consistent default gateway, while DHCP was used for endpoints to simplify
host management and reduce configuration errors.

---

## pfSense Configuration

### Interface Assignment
- WAN interface configured for DHCP (VirtualBox NAT)
- LAN interface configured with a static IP address
- LAN connected to an Internal Network (`soc_lan`)

---

### DHCP Configuration
- DHCP server enabled on the LAN interface
- Address pool configured from 192.168.10.100 to 192.168.10.200
- pfSense acts as the sole DHCP authority for all internal hosts

This ensured that all systems automatically received an IP address,
default gateway, and DNS configuration.

---

### DNS Configuration
The pfSense DNS Resolver (Unbound) was enabled in forwarding mode.
All LAN clients use pfSense as their DNS server, allowing centralized
name resolution and improved visibility into DNS traffic.

---

## Connectivity Verification

### IP Assignment Verification
Each system successfully obtained an IP address within the
192.168.10.0/24 subnet, confirming that DHCP was functioning correctly.

---

### Ping Tests
Connectivity was verified using ICMP:
- Host to pfSense
- Host to host
- Host to Internet (8.8.8.8)
- DNS resolution tested using domain name pings

Successful responses confirmed proper routing and DNS functionality.

---

### Traceroute Test
A traceroute was performed from Kali Linux to the Ubuntu Server to verify
that internal traffic remained within the LAN and did not traverse the WAN.

```bash
traceroute <ubuntu-ip>
## Troubleshooting Highlights
During the lab, several real-world issues were encountered and resolved:

- DHCP failures caused by mismatched VirtualBox Internal Network names
- APIPA (169.254.x.x) addresses indicating DHCP unreachability
- LAN interface misconfiguration during pfSense setup
- DNS service conflicts between DNS Resolver and DNS Forwarder

These issues were resolved through systematic Layer 2 and Layer 3 troubleshooting.

---

## Skills Demonstrated
- Network design and segmentation
- Firewall deployment and interface configuration
- DHCP and DNS service implementation
- Virtual switching concepts
- Network troubleshooting methodology
- Technical documentation
