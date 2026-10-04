# Case 001: Windows Network Connectivity Troubleshooting

## 📋 Overview
* **Environment:** Windows 11 / Remote Workstation
* **Severity:** High (Sudden loss of internet and network resource access)
* **Status:** Resolved
* **Tools Used:** `ipconfig`, `ping`, `nslookup`, `Test-NetConnection`

---

## 1. Problem
The user experienced a sudden loss of internet connectivity and was unable to access internal web applications or external websites while working remotely.

## 2. Symptoms
* Web browsers display errors such as `DNS_PROBE_FINISHED_NXDOMAIN` or `This site can't be reached`.
* Collaboration and cloud synchronization tools fail to connect.
* Local network shared drives become inaccessible.

## 3. Initial Assessment
Verified that the physical network adapter / Wi-Fi interface was physically/logically enabled. The network icon showed a connected status, but data packets were failing to route externally, requiring a systematic diagnostic procedure.

## 4. Commands Executed & Investigation

1. **Local TCP/IP Stack Verification:**
   * Executed `ping 127.0.0.1` to ensure the local loopback interface and TCP/IP stack were functioning correctly.
   
   <img width="455" height="129" alt="Captura de pantalla 2026-10-03 182727" src="https://github.com/user-attachments/assets/dff73bb4-aeae-4aca-80da-294474730c45" />
   
2. **IP Configuration & Gateway Check:**
   * Executed `ipconfig /all` to review IPv4 address assignment, subnet mask, default gateway, and assigned DNS servers.

<img width="718" height="388" alt="image" src="https://github.com/user-attachments/assets/f112fb0d-f2c0-4d15-85e0-7feb2f9d4e00" />

   
3. **External IP Routing Test:**
   * Executed `ping 8.8.8.8` to test direct routing to external public IP addresses, bypassing DNS variables.

<img width="470" height="179" alt="image" src="https://github.com/user-attachments/assets/e11de7b2-ce0c-42fd-a8a9-4912d875e8db" />

   
4. **Name Resolution (DNS) Investigation:**
   * Executed `nslookup google.com` to verify if the configured DNS server could successfully translate domain names to IP addresses.

<img width="445" height="141" alt="image" src="https://github.com/user-attachments/assets/623f3590-6204-42ad-ab2e-82e36f402b84" />

   
5. **Port Reachability & TCP Handshake:**
   * Executed `Test-NetConnection google.com -Port 443` in PowerShell to test TCP port 443 connectivity and outbound security traversal.

<img width="521" height="141" alt="image" src="https://github.com/user-attachments/assets/3ba2dae3-c70e-435d-9000-108e50ac467d" />


## 5. Root Cause
Stale DNS cache entries combined with a temporary DHCP gateway timeout, causing name resolution failure and packet dropping at the network layer.

## 6. Resolution
1. Cleared the local DNS resolver cache to purge corrupted records:
   ```cmd
   ipconfig /flushdns
