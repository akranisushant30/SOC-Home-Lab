🎯 Attack Phase 1 — Reconnaissance

This phase focused on identifying active systems within the lab network and discovering exposed services on the target server. The activity was performed from the Kali Linux attacker machine against the Ubuntu Server hosted inside the VMware NAT environment.

🔍 Host Discovery

I first performed network reconnaissance using Netdiscover to identify all live hosts in the 192.168.67.0/24 subnet.

netdiscover -r 192.168.67.0/24

The scan revealed multiple active systems, including the target Ubuntu server at 192.168.67.128. This confirmed that the host was reachable and available for further enumeration.

🛰️ Service Enumeration

After identifying the target IP, I executed a full TCP port and service version scan using Nmap.

nmap -sV -p- 192.168.67.128

📌 Key Findings

Port 22/tcp — OpenSSH 8.9p1

Port 80/tcp — Apache HTTP Server 2.4.52

Operating System — Ubuntu Linux

The Nmap scan showed that SSH and HTTP services were publicly accessible on the target server, making them potential entry points for subsequent attack phases such as web enumeration and credential-based attacks.
