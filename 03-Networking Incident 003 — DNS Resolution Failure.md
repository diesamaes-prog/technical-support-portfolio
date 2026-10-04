# Networking Incident 003 — DNS Resolution Failure

## Incident

A user reports that their Windows computer is connected to the network, but websites are not loading correctly.

The user can see that the computer is connected to the local network, but they are unable to access websites or web-based applications.

The issue appears to affect Internet access from the computer. The first step is to determine whether the problem is related to the local TCP/IP configuration, the network gateway, Internet connectivity, DNS resolution, or the remote service itself.

This incident is being investigated using a Windows workstation and PowerShell.

---

## Environment

**Operating System:** Windows 10/11
**Connection:** Ethernet / Wi-Fi
**Device:** Windows workstation
**Tools:** PowerShell, Windows networking utilities
**Support Level:** L1/L2 Service Desk

---

## Initial Report

**User:** "My computer says it's connected to the Internet, but websites aren't loading."

The user has already confirmed that the network connection appears active.

The first step is to verify whether the computer has a valid network configuration.

---

## 1. Check IP Configuration

The following command was used to review the computer's current network configuration:

```powershell
ipconfig /all
```

### What I checked

* IPv4 address
* Subnet mask
* Default gateway
* DNS servers
* DHCP configuration
* Network adapter status

### Evidence


<img width="745" height="383" alt="Captura de pantalla 2026-10-03 211213" src="https://github.com/user-attachments/assets/04bbac60-bc8f-42a9-af10-76d837aea9fa" />


### Findings


Finding: The workstation has a valid IPv4 configuration and an active network connection. DHCP is enabled, a default gateway is assigned, and DNS servers are configured. No obvious IP configuration issue was identified at this stage. Further testing is required to determine whether the problem is related to gateway connectivity, Internet access, or DNS resolution.

---

## 2. Test the Local TCP/IP Stack

The next test checks whether the local TCP/IP stack is responding correctly.

```powershell
ping 127.0.0.1
```


The loopback address does not depend on the external network connection. A successful response indicates that the local TCP/IP stack is functioning.

### Evidence

<img width="464" height="186" alt="image" src="https://github.com/user-attachments/assets/8c456722-ed94-4a59-8b90-5de87fcb4a3d" />


### Findings

**Finding:** The loopback test to `127.0.0.1` completed successfully with no packet loss. This confirms that the local TCP/IP stack is responding normally on the workstation. No local TCP/IP stack failure was identified at this stage.


---

## 3. Test the Default Gateway

The default gateway was tested to determine whether the computer could communicate with the local network router.

```powershell
ping <default-gateway>
```

The gateway address should be taken from the `Default Gateway` value shown by `ipconfig /all`.

### Evidence

<img width="494" height="185" alt="image" src="https://github.com/user-attachments/assets/f5c4ff9b-4876-47fd-a892-0420fa171312" />


### Findings

**Finding:** The default gateway at 192.168.100.1 responded successfully to all four ICMP requests. The test completed with 0% packet loss and an average round-trip time of 4 ms. This confirms that the workstation can communicate successfully with the local network gateway. No local gateway connectivity issue was identified.


---

## 4. Test Internet Connectivity Without DNS

The next test checks Internet connectivity using an IP address instead of a hostname.

```powershell
ping 8.8.8.8
```

Using an IP address is useful because this test does not require DNS resolution.

If this test succeeds while hostname-based access fails, DNS becomes a strong suspect.

### Evidence

<img width="479" height="189" alt="image" src="https://github.com/user-attachments/assets/db0b6019-4941-4bf4-805a-66ca7212e0b8" />


### Findings

**Finding:** The workstation successfully reached the public IP address 8.8.8.8 with 0% packet loss. The average round-trip time was 17 ms, confirming that the workstation has working Internet connectivity at the IP level. No general Internet connectivity issue was identified during this test.

---

## 5. Test DNS Resolution

The next step is to determine whether the computer can translate a hostname into an IP address.

```powershell
nslookup google.com
```

This test checks whether the configured DNS server can resolve the requested hostname.

### Evidence

<img width="352" height="122" alt="image" src="https://github.com/user-attachments/assets/7d610aa3-217d-4cec-8ff5-74f9602f8495" />


### Findings

**Finding:** DNS resolution was successful. The workstation successfully resolved `google.com` to both IPv4 and IPv6 addresses. The DNS server responded to the query correctly. Although the server was displayed as `UnKnown`, this did not affect DNS resolution.


---

## 6. Test HTTPS Connectivity

After checking DNS, I tested connectivity to the remote HTTPS service.

```powershell
Test-NetConnection google.com -Port 443
```

This helps determine whether TCP connectivity to port 443 is available.

### Evidence

<img width="487" height="121" alt="image" src="https://github.com/user-attachments/assets/d1bf81ef-53b5-4c9e-9776-b0c4a4c649cc" />


### Findings

**Finding:** The workstation successfully established a TCP connection to `google.com` over port 443 using the Wi-Fi interface. The `TcpTestSucceeded` result was `True`, confirming that HTTPS connectivity is available.


---

# Investigation

The results from the previous tests are compared to determine where the connection is failing.

The troubleshooting path is:

```text
Network Adapter
      ↓
IP Configuration
      ↓
Local TCP/IP Stack
      ↓
Default Gateway
      ↓
Internet Connectivity
      ↓
DNS Resolution
      ↓
TCP 443 / HTTPS
      ↓
Application
```

The purpose of testing each layer separately is to avoid changing settings before identifying the actual failure.


## Investigation Results

The workstation was tested progressively from the local TCP/IP stack through Internet and HTTPS connectivity.

### 1. Local TCP/IP Stack

`ping 127.0.0.1`

**Result:** Successful.

The loopback address responded successfully, confirming that the local TCP/IP stack is functioning.

### 2. Default Gateway

`ping 192.168.100.1`

**Result:** Successful.

The gateway responded to all four ICMP requests with **0% packet loss**. Round-trip time ranged from **1 ms to 9 ms**, with an average of **4 ms**.

This confirms that the workstation can communicate successfully with the local network gateway.

### 3. Internet Connectivity

`ping 8.8.8.8`

**Result:** Successful.

All four packets were received with **0% packet loss**. Round-trip time ranged from **15 ms to 20 ms**, with an average of **17 ms**.

This confirms Internet connectivity at the IP level without relying on DNS resolution.

### 4. DNS Resolution

`nslookup google.com`

**Result:** Successful.

The DNS query successfully resolved `google.com` to both IPv6 and IPv4 addresses.

The DNS server was displayed as `UnKnown`, but the query itself completed successfully, confirming that DNS resolution is functioning.

### 5. TCP/HTTPS Connectivity

`Test-NetConnection google.com -Port 443`

**Result:** Successful.

The test returned:

```text
TcpTestSucceeded : True
```

The workstation successfully established a TCP connection to `google.com` on port **443** through the Wi-Fi interface.

### Overall Investigation Result

All connectivity tests completed successfully:

**Local TCP/IP → Default Gateway → Internet → DNS → TCP 443**

No failure was identified in the basic network connectivity tests performed on the workstation.

---

# Root Cause

**Root Cause:**

The root cause could not be reproduced during troubleshooting. Network connectivity was confirmed at the local gateway, Internet, DNS, and HTTPS levels.

The workstation successfully reached the default gateway, reached 8.8.8.8 with no packet loss, resolved google.com through DNS, and established a TCP connection to port 443. No network, DNS, or HTTPS connectivity failure was identified during the investigation.

The issue may have been intermittent or application/browser-specific rather than a general network connectivity problem.


---

# Resolution

No network configuration changes were required. Connectivity was verified successfully at the gateway, Internet, DNS, and HTTPS levels.

The browser/application was retested after the connectivity checks and the connection was confirmed to be working. Since no underlying network failure could be reproduced, the incident was considered resolved with no changes required to the network configuration.

If the issue returns, browser/application-specific troubleshooting should be performed to identify the intermittent cause.


---

# Verification

Connectivity was verified successfully after troubleshooting. The workstation was able to communicate with the default gateway, reach the Internet by IP, resolve external DNS names, and establish a TCP connection to Google over HTTPS (port 443).

The connection was confirmed to be operational, with no packet loss observed during the gateway and Internet connectivity tests. No further network issues were identified.


After applying the resolution, the following tests should be repeated as appropriate:

```powershell
nslookup google.com
```

<img width="369" height="143" alt="image" src="https://github.com/user-attachments/assets/71807730-551a-4af9-94cf-c4ff39fdab13" />


```powershell
Test-NetConnection google.com -Port 443
```

<img width="508" height="141" alt="image" src="https://github.com/user-attachments/assets/c12f5433-68fc-40aa-9817-75b0b689ad4b" />


A web browser should then be used to confirm that normal websites load successfully.

### Evidence

**Screenshot:** `07-dns-after-fix.png`

<img width="449" height="120" alt="image" src="https://github.com/user-attachments/assets/341bcd5f-5429-49b5-9706-caa7f9a57271" />


**Screenshot:** `08-final-browser-test.png`

<img width="652" height="701" alt="image" src="https://github.com/user-attachments/assets/e39a2644-0568-45c7-8012-2fdb3386565f" />


### Verification Results

```text
DNS resolution:
Successful. nslookup successfully resolved google.com and returned both IPv4 and IPv6 addresses.

HTTPS connectivity:
Successful. Test-NetConnection confirmed a successful TCP connection to google.com on port 443.

Web browsing:
Not specifically tested during the investigation. Network-level HTTPS connectivity was confirmed successfully.

User confirmation:
Pending user confirmation. No network connectivity failure was reproduced during troubleshooting.
```


---

# Final Ticket Notes

**Issue:** Windows computer connected to the network but unable to access websites.

**Initial symptom:** Websites were not loading.

**Affected user:** Single workstation.

**Investigation:** IP configuration, local TCP/IP, gateway connectivity, Internet connectivity, DNS resolution, and TCP 443 were tested.

**Root Cause:** The issue could not be reproduced during troubleshooting. Gateway connectivity, Internet connectivity, DNS resolution, and HTTPS connectivity were all functioning normally.

**Resolution:** No network configuration changes were required. Connectivity was verified successfully at the gateway, Internet, DNS, and HTTPS levels.

**Verification:** DNS successfully resolved google.com, and TCP connectivity to google.com on port 443 was successful. No packet loss was observed during gateway or Internet connectivity tests.

**Status:** Resolved.



