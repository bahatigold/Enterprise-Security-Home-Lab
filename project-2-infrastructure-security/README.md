# Hardened Enterprise Infrastructure & Secure Access Lab

## Objective
The objective of this project was to architect a secure, resilient, and segmented enterprise network environment. The focus was on implementing strict access controls, identity management, and secure remote connectivity using industry-standard tools.

## Architecture & Technologies Used
*   **Perimeter Defense:** pfSense Next-Generation Firewall (NGFW)
*   **Identity & Access Management (IAM):** Windows Server (Active Directory Domain Controller)
*   **Secure Remote Access:** OpenVPN with self-managed PKI/Certificate Authority
*   **Endpoints:** Windows 10/11 Clients
*   **Offensive Validation:** Kali Linux

## Key Configurations & Security Controls

### 1. Network Segmentation & Firewall Policies
*   Architected a multi-LAN environment via pfSense, strictly separating the Server infrastructure (LAN 1) from Client endpoints (LAN 2).
*   Implemented schedule-based Access Control Lists (ACLs) and web filtering aliases to block unauthorized outbound traffic (e.g., social media platforms) during business hours.

### 2. Active Directory Hardening
*   Promoted a Windows Server to a Domain Controller to centralize authentication.
*   Enforced strict Group Policy Objects (GPOs), including:
    *   Minimum password complexity of 12+ characters.
    *   Account lockout thresholds (e.g., lock after 3 failed attempts) to mitigate brute-force attacks.
    *   Centralized NTP synchronization to ensure temporal accuracy for forensic logging.

### 3. Secure Remote Connectivity
*   Deployed an OpenVPN server on the pfSense perimeter.
*   Generated and managed a Certificate Authority (CA) to issue unique client certificates, ensuring encrypted, authenticated remote access for administrative users.

## Defensive Validation
To ensure the infrastructure was properly hardened, I conducted validation testing from an isolated Kali Linux machine:
*   **Nmap Scanning:** Executed -sS (Stealth SYN) and -Pn (No Ping) scans to verify that firewall drop rules were successfully masking internal assets and that unauthorized subnets were unreachable.
*(Insert Screenshot of Kali Linux terminal showing blocked scan results or pfSense firewall drop logs here)*

## Challenges & Lessons Learned
*   **GPO Troubleshooting:** Learned how to use `gpupdate /force` and `rsop.msc` to troubleshoot policies that weren't applying correctly to the client VMs.
*   **VPN Routing:** Gained a deeper understanding of network routing and NAT when configuring the OpenVPN tunnel to allow access to specific internal subnets without exposing the whole network.
