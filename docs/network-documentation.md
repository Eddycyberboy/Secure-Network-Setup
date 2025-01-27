# Secure Network Setup for a Small Business or Home Office

## Overview
This project outlines the design, implementation, and security measures for a secure network that includes a firewall, VPN server, IDS/IPS, VLANs, and a DMZ. The setup ensures secure access, isolates sensitive data, and detects potential threats.

---

## Network Diagram
![Secure-Network project diagram](https://github.com/user-attachments/assets/e01776ce-1d69-4419-ae6c-300d84ad7c82)


---

## Subnet and IP Allocation
| **Zone**       | **Subnet**         | **Purpose**                                             |
|-----------------|--------------------|---------------------------------------------------------|
| WAN Zone        | `192.168.0.0/24`  | Connects the internal network to the Internet.          |
| LAN Zone        | `192.168.1.0/24`  | Contains internal devices such as file servers, workstations, and IoT devices. |
| DMZ Zone        | `192.168.2.0/24`  | Hosts public-facing servers, like a web server.         |
| Guest Wi-Fi     | `192.168.10.0/24` | Isolated network for guest devices.                     |

---

## Network Components

### Router
- **Role:** Acts as the gateway to the Internet.
- **Purpose:** Directs traffic between the WAN and internal network.
- **WAN Interface IP:** `192.168.0.1`
- **LAN Interface IP:** `192.168.1.1`

### Firewall
- **Role:** Protects the network by enforcing traffic rules.
- **Purpose:**
  - Filters incoming and outgoing traffic.
  - Blocks unauthorized access to sensitive zones.
- **Interfaces:**
  - WAN: `192.168.0.254`
  - LAN: `192.168.1.1`
  - DMZ: `192.168.2.1`

### VPN Server
- **Role:** Provides secure remote access to the LAN.
- **Purpose:** Encrypts remote connections to protect data in transit.
- **IP Address:** `192.168.1.10`

### IDS/IPS
- **Role:** Monitors network traffic for threats and anomalies.
- **Purpose:** Detects and blocks malicious activities like port scans.
- **IP Address:** `192.168.1.20`

### DMZ Servers
#### Web Server
- **Role:** Hosts public-facing websites.
- **Purpose:** Provides external users access to web services without exposing the LAN.
- **IP Address:** `192.168.2.1`

---

## Firewall Rules
| **Traffic**         | **Source**       | **Destination**  | **Protocol/Ports** | **Action**      |
|---------------------|------------------|------------------|---------------------|-----------------|
| Public Access       | WAN              | DMZ (192.168.2.1)| HTTP/HTTPS (80/443)| Allow           |
| DMZ Isolation       | DMZ              | LAN              | Any                | Deny            |
| Internal Access     | LAN              | DMZ              | SSH, Management    | Allow           |
| Internet Access     | LAN, DMZ         | WAN              | Any                | Allow           |
| Guest Isolation     | Guest VLAN       | LAN              | Any                | Deny            |

---

## VLAN Segmentation
- **VLAN 1 (LAN Devices):** Internal devices (workstations, file servers).
- **VLAN 2 (Guest Wi-Fi):** Isolated network for guest access.
- **VLAN 3 (DMZ):** Public-facing servers like the web server.

---

## Security Measures
### Encryption
- The VPN uses AES-256 encryption for remote connections.

### Traffic Segmentation
- VLANs and subnets ensure that traffic is isolated between zones.

### Threat Detection
- The IDS/IPS monitors LAN traffic for malicious activity.

### Firewall Rules
- Strictly controls traffic between WAN, LAN, and DMZ.

---

## Testing and Validation
### Penetration Testing Tools
- Used **Nmap** to scan for open ports.
- Tested firewall rules using **Metasploit**.

### IDS/IPS Validation
- Simulated port scans and brute-force attacks to ensure the IDS detected threats.

---

## Challenges and Lessons Learned
### Challenges
- Configuring the firewall to allow DMZ traffic while blocking unauthorized access to the LAN.

### Lessons Learned
- Ensured clear separation of zones by double-checking firewall rules and VLAN configurations.

---

## Conclusion
The secure network setup provides a robust solution for a small business or home office. With its segmented zones, encrypted VPN access, and intrusion detection system, it ensures data security, threat detection, and reliable remote access.

