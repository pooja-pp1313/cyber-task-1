# Cyber Security Internship – Task 1

###  Task: Port Scanning Your Local Network

**Tools Used:**
- Nmap (TCP SYN Scan)
- Wireshark

**IP Range Scanned:** `192.168.1.0/24`  
**Command Used:** nmap -sS 192.168.1.0/24 -oN scan_results.txt


---

###  Nmap Findings:

| IP Address    | Open Ports             | Services                    |
|---------------|------------------------|-----------------------------|
| 192.168.1.1   | 53, 80, 443            | DNS, HTTP, HTTPS            |
|               | 21, 22, 23 (filtered)  | FTP, SSH, Telnet (filtered) |
| 192.168.1.2   | 135, 139, 445          | MSRPC, NetBIOS, SMB         |

---

### 🔐 Risk Analysis:

- **192.168.1.1**
  - Ports 21/22/23 are filtered — might be vulnerable if open
  - Ports 80/443 — typically web services, could expose admin panels
  - Port 53 — if DNS is open, can be abused for poisoning or tunneling

- **192.168.1.2 (my system)**
  - Port 445 — widely targeted in ransomware (e.g., WannaCry)
  - Ports 135/139 — used for NetBIOS/SMB, exploitable inside LANs

---

###  Wireshark Packet Capture

- **File**: `capture.pcapng`
- **Purpose**: Shows Nmap sending TCP SYN packets (stealth scan)
- **Filter used**: tcp.flags.syn == 1 && tcp.flags.ack == 0


- This filter reveals all the **initial connection attempts (SYN)** sent by Nmap.
- Helps confirm how SYN scan probes devices without completing a full TCP handshake.

---

###  Learning Outcome:
- Learned to use Nmap to detect open ports in local network
- Understood the role of TCP SYN scan in stealthy enumeration
- Used Wireshark to observe packet behavior during scan
- Gained basic knowledge of service exposure and potential risks



