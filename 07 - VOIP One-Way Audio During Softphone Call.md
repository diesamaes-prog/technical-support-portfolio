# VoIP Incident 001 — Zoiper5 One-Way Audio During VoIP Call

**Category:** VoIP / Softphone
**Application:** Zoiper5
**Severity:** Medium
**Status:** In Progress
**Environment:** Windows workstation

## Issue

User reports that a VoIP call can be established through **Zoiper5**, but audio is not working correctly. The user can hear the remote party, but the remote party cannot hear the user.

## Initial Symptom

Zoiper5 is configured with a SIP account and is expected to establish VoIP calls normally. The user reports **one-way audio** during calls.

The issue may be related to the microphone configuration, Windows microphone permissions, Zoiper5 audio-device settings, SIP/RTP communication, network connectivity, or another component of the VoIP audio path.

---

# Investigation

### Step 1 — Verify Zoiper5 SIP Registration

Open Zoiper5 and review the configured SIP account.

Confirm the account status:

* Registered / Online
* Unregistered
* Registration failed
* Disabled
* Other status

**Evidence:**



<img width="836" height="576" alt="image" src="https://github.com/user-attachments/assets/81021d25-3e92-4c6b-a549-22e2f44d8585" />


**Notes:**

Account status is registered as confirmed by checkmark next to the I.P.

> Do not expose SIP passwords, authentication secrets, or other credentials.

---

### Step 2 — Verify Local Network Connectivity

Open Command Prompt and run:

```cmd
ipconfig
```

Identify the active network adapter and default gateway.

Then test the gateway:

```cmd
ping <default-gateway>
```



Example:

```cmd
ping 192.168.100.1
```




Record the actual result.

**Evidence:**

<img width="640" height="292" alt="image" src="https://github.com/user-attachments/assets/f2d2bb32-8644-4603-848e-b0d431a436ac" />

<img width="536" height="243" alt="image" src="https://github.com/user-attachments/assets/d8802e2b-180c-438a-b21d-3b3e1e5dab7d" />


**Finding:**

Estadísticas de ping para 192.168.100.1:
    Paquetes: enviados = 4, recibidos = 4, perdidos = 0
    (0% perdidos),
Tiempos aproximados de ida y vuelta en milisegundos:
    Mínimo = 4ms, Máximo = 9ms, Media = 6ms

---

### Step 3 — Verify Internet Connectivity

Run:

```cmd
ping 8.8.8.8
```

Record:

* Packets sent
* Packets received
* Packet loss
* Minimum latency
* Maximum latency
* Average latency

**Evidence:**

`03-internet-connectivity.png`

**Screenshot:**

<img width="469" height="219" alt="image" src="https://github.com/user-attachments/assets/1e51c55a-2137-438b-b1a1-420772d2f2f2" />


**Finding:**

Haciendo ping a 8.8.8.8 con 32 bytes de datos:
Respuesta desde 8.8.8.8: bytes=32 tiempo=19ms TTL=117
Respuesta desde 8.8.8.8: bytes=32 tiempo=15ms TTL=117
Respuesta desde 8.8.8.8: bytes=32 tiempo=16ms TTL=117
Respuesta desde 8.8.8.8: bytes=32 tiempo=15ms TTL=117

Estadísticas de ping para 8.8.8.8:
    Paquetes: enviados = 4, recibidos = 4, perdidos = 0
    (0% perdidos),
Tiempos aproximados de ida y vuelta en milisegundos:
    Mínimo = 15ms, Máximo = 19ms, Media = 16ms

---

### Step 4 — Verify DNS Resolution

Run:

```cmd
nslookup google.com
```

Confirm that the DNS query returns an address.

**Evidence:**

`04-dns-resolution.png`

**Screenshot:**

<img width="472" height="159" alt="image" src="https://github.com/user-attachments/assets/1a735911-79b8-4e0d-8fbe-53f51a28a9ee" />


**Finding:**

PS C:\WINDOWS\system32> nslookup google.com
Servidor:  UnKnown
Address:  2806:2f0:61::11

Respuesta no autoritativa:
Nombre:  google.com
Addresses:  2607:f8b0:4012:82a::200e
          192.178.57.46

PS C:\WINDOWS\system32>

---

### Step 5 — Verify SIP Connectivity

If the Zoiper5 account provides a legitimate SIP server/host, identify the configured SIP server and port.

Common SIP ports include:

* UDP/TCP 5060
* TLS 5061

Use the **actual server and port configured for the Zoiper5 account**.

For TCP-based testing:

```powershell
Test-NetConnection <sip-server> -Port <port>
```

Example:

```powershell
Test-NetConnection sip.example.com -Port 5060
```

Do **not** use a random public SIP server simply to manufacture a test result.

If the configured SIP service does not provide a TCP testable endpoint, document that limitation.

**Evidence:**

What we just established

Your output shows:

PingSucceeded: True
RTT: 58 ms
TcpTestSucceeded: False
Port tested: TCP 5060

So your computer can reach 199.7.85.135 at the IP level, but a TCP connection to port 5060 was not established.

That does not automatically mean the SIP service is down. SIP 5060 is very commonly used over UDP, and Test-NetConnection -Port tests TCP.



**Screenshot:**

<img width="599" height="237" alt="image" src="https://github.com/user-attachments/assets/83be49fe-bab6-410e-a8f2-8d7b1e0d020a" />



**Finding:**

The SIP server 199.7.85.135 responded to ICMP ping with an average latency of 58 ms, confirming IP-level reachability. However, a TCP connection to port 5060 could not be established. Because SIP may operate over UDP on port 5060, the TCP test alone does not confirm that SIP connectivity is unavailable. Further verification through Zoiper5 registration status is required.

---

### Step 6 — Verify Windows Audio Devices

Open:

**Settings → System → Sound**

Check the configured:

**Input**

Confirm that the correct microphone is selected.

**Output**

Confirm that the correct speakers/headset are selected.

Verify that the microphone is not muted.

**Evidence:**

`06-audio-device-configuration.png`

**Screenshot:**

<img width="445" height="285" alt="image" src="https://github.com/user-attachments/assets/476c9f34-c096-45e2-84c8-58636af263ae" />


**Finding:**

The Computer is taking the headset as the output device

---

### Step 7 — Test the Microphone

Use the Windows microphone test or another legitimate local audio test.

Confirm that Windows can detect microphone input.

Record the actual result.

**Evidence:**

`07-microphone-test.png`

**Screenshot:**

<img width="470" height="408" alt="image" src="https://github.com/user-attachments/assets/7156f922-a1bb-481c-8f64-8d31c96ce87d" />


**Finding:**

The computer is taking the headset as the input device

---

### Step 8 — Verify Microphone Permissions

Open:

**Settings → Privacy & security → Microphone**

Verify:

* Microphone access — enabled
* Let apps access your microphone — enabled
* Let desktop apps access your microphone — enabled

Zoiper5 is a desktop application, so desktop microphone access is particularly relevant.

**Evidence:**

`08-microphone-permission.png`

**Screenshot:**

<img width="480" height="429" alt="image" src="https://github.com/user-attachments/assets/ae55ba64-4860-4d9c-93cc-6c22922f66a1" />


**Finding:**

The permission for the Microphone and speakers is toggled on.

---

### Step 9 — Perform Controlled Zoiper5 Test Call

Perform a legitimate test call using the configured Zoiper5 account.

<img width="953" height="578" alt="image" src="https://github.com/user-attachments/assets/6be3178c-ef69-4ce6-a5f7-e4ecb4f9583f" />


Document exactly what happens.

Possible results:

Finding: The SIP server 199.7.85.135 is reachable at the IP level, with successful ICMP response (58 ms RTT). However, the TCP connection test to port 5060 failed. A test call through Zoiper5 was subsequently rejected. This indicates that basic IP connectivity is available, but the SIP call could not be established successfully. Further investigation of Zoiper5 SIP registration, account configuration, SIP signaling, and the configured SIP service is required.
