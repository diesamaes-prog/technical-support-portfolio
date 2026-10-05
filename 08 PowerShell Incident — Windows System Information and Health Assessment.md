# PowerShell Incident 001 — Windows System Information and Health Assessment

**Category:** PowerShell / Windows Administration
**Application:** Windows PowerShell
**Severity:** Low
**Status:** In Progress
**Environment:** Windows workstation

## Issue

A user reports that their Windows workstation has been experiencing intermittent performance issues. The Service Desk needs to collect system information and perform an initial health assessment before determining whether further troubleshooting or escalation is required.

## Initial Symptom

The workstation is reported as slower than usual during normal use.

No specific hardware failure, application error, or network outage has been reported at the beginning of the investigation.

PowerShell will be used to collect system information, resource utilization, storage status, network configuration, running processes, and relevant Windows services.

---

# Investigation

## Step 1 — Identify the Workstation

Run:

```powershell
Get-ComputerInfo | Select-Object CsName, WindowsProductName, WindowsVersion, OsBuildNumber
```

Record:

CsName          WindowsProductName WindowsVersion OsBuildNumber
------          ------------------ -------------- -------------
DESKTOP-Q2MV7OV Windows 10 Pro     2009           26200

**Evidence:**

<img width="666" height="163" alt="image" src="https://github.com/user-attachments/assets/c006ba4d-7dbc-4c84-bc52-76ca30ca4549" />


**Finding:**

Finding: The workstation is identified as DESKTOP-Q2MV7OV and is running Windows 10 Pro, version 2009, build 26200. The operating system information was successfully retrieved through PowerShell, confirming that PowerShell can query the workstation's system inventory.

---

## Step 2 — Identify the Current User

Run:

```powershell
whoami
```

Then:

```powershell
$env:USERNAME
```

This confirms the account currently being used on the workstation.

**Evidence:**

<img width="263" height="43" alt="image" src="https://github.com/user-attachments/assets/c6ecf303-35b7-4750-9ec2-4180d4772918" />

<img width="302" height="29" alt="image" src="https://github.com/user-attachments/assets/89a09e5c-260e-4f93-8537-5355f5c8cafb" />


**Finding:**

Finding: The current session is running under the local Windows account usuario. The results from whoami and $env:USERNAME are consistent, so there is no discrepancy in the account identification.

> Redact your username if you publish the screenshot publicly.

---

## Step 3 — Check CPU Information

Run:

```powershell
Get-CimInstance Win32_Processor |
Select-Object Name, NumberOfCores, NumberOfLogicalProcessors, MaxClockSpeed
```

Record the processor model and available cores/threads.

**Evidence:**

<img width="729" height="212" alt="image" src="https://github.com/user-attachments/assets/01a8b525-cd91-4cdf-86ea-dbd2c31bff2f" />


**Finding:**

Finding: The system is using a 2-core/4-thread mobile Intel processor. PowerShell successfully retrieved the processor information, and there is no indication of a CPU detection or hardware-reporting issue.

For the incident, this establishes the workstation's CPU baseline. The relatively older/lower-power processor could contribute to performance limitations under heavier workloads, but we cannot identify it as the cause of the reported intermittent performance issue yet.
---

## Step 4 — Check Memory

Run:

```powershell
Get-CimInstance Win32_ComputerSystem |
Select-Object TotalPhysicalMemory
```

For a more readable result:

```powershell
"{0:N2} GB" -f ((Get-CimInstance Win32_ComputerSystem).TotalPhysicalMemory / 1GB)
```

Record the installed physical memory.

**Evidence:**

<img width="844" height="174" alt="image" src="https://github.com/user-attachments/assets/bae1a910-d5f7-4088-80c5-a123400bd39b" />


**Finding:**

Installed physical RAM: 12 GB approximately
PowerShell-reported: 11.91 GB

Finding: The workstation has approximately 12 GB of installed RAM, which is adequate for basic Windows 10 usage and standard Service Desk tasks. However, it may become a performance limitation when running multiple applications or resource-intensive workloads simultaneously.

There is no indication of a memory detection problem. This step establishes the installed-memory baseline; we still need to check how much memory is actually available/in use.

---

## Step 5 — Check Current Memory Usage

Run:

```powershell
Get-CimInstance Win32_OperatingSystem |
Select-Object `
@{Name="TotalMemoryGB";Expression={[math]::Round($_.TotalVisibleMemorySize/1MB,2)}},
@{Name="FreeMemoryGB";Expression={[math]::Round($_.FreePhysicalMemory/1MB,2)}}
```

This allows us to compare total and available physical memory.

**Evidence:**

<img width="860" height="105" alt="image" src="https://github.com/user-attachments/assets/5b544a3a-9b43-4ce1-a0be-687d5547fe9f" />


**Finding:**

Finding: The workstation currently has approximately 3.47 GB of RAM available, with about 70.9% of physical memory in use. This indicates moderately high memory utilization, but it does not by itself establish a memory-related performance problem.

This is useful as a baseline for the intermittent-performance investigation.

---

## Step 6 — Check Disk Space

Run:

```powershell
Get-PSDrive -PSProvider FileSystem
```

For the Windows system drive:

```powershell
Get-PSDrive C |
Select-Object Name,
@{Name="UsedGB";Expression={[math]::Round($_.Used/1GB,2)}},
@{Name="FreeGB";Expression={[math]::Round($_.Free/1GB,2)}}
```

Record the available space.

**Evidence:**

<img width="858" height="107" alt="image" src="https://github.com/user-attachments/assets/70fc3c48-8c64-4a00-bcb9-6db6dc33c8ec" />


**Finding:**

Drive: C:
Used: 62.01 GB
Free: 384.07 GB
Total: ≈ 446.08 GB
Free space: ≈ 86%

Finding: The C: drive has approximately 384 GB of free space, so there is no indication of insufficient disk space contributing to the reported performance issue.

This is a healthy result and effectively rules out low storage as a likely cause at this stage.

---

## Step 7 — Check Network Configuration

Run:

```powershell
Get-NetIPConfiguration
```

Review:

* Network adapter
* IPv4 address
* Default gateway
* DNS servers

**Evidence:**

<img width="613" height="442" alt="image" src="https://github.com/user-attachments/assets/fbf70409-1524-4221-add4-6c4f36ac16d9" />


**Finding:**

The workstation's active network configuration is:

Active interface: Wi-Fi
Adapter: Qualcomm Atheros AR956x Wireless Network Adapter
IPv4: 192.168.100.4
IPv4 Gateway: 192.168.100.1
DNS servers: Configured and present
Ethernet: Disconnected
Bluetooth PAN: Disconnected

Finding: The workstation has an active Wi-Fi connection with a valid IPv4 address, default gateway, and DNS configuration. The Ethernet and Bluetooth interfaces are disconnected, which is normal and does not indicate a problem by itself.

> Redact public IP addresses before publishing the screenshot.

---

## Step 8 — Test Network Connectivity

Test the local gateway:

```powershell
Test-Connection <DEFAULT-GATEWAY> -Count 4
```

Then test an external IP:

```powershell
Test-Connection 8.8.8.8 -Count 4
```

Use the **actual default gateway discovered in Step 7**.

**Evidence:**

<img width="852" height="525" alt="image" src="https://github.com/user-attachments/assets/d736ca15-4355-4195-8671-fd72c59e0513" />


**Finding:**

The Internet connectivity test produced 3 successful replies before the fourth attempt returned a local PingException:

Reply 1: 16 ms
Reply 2: 19 ms
Reply 3: 20 ms
Attempt 4: Error — “falta de recursos”

Finding: Internet connectivity is working, because the workstation successfully reached 8.8.8.8 three times with low latency. The fourth attempt failed locally with a resource-related PowerShell error, but this does not establish an Internet outage or network failure.

Combined with the successful gateway test, the workstation has demonstrated:

Workstation → Wi-Fi → Gateway → Internet: functional

We should document the fourth-attempt error rather than ignoring it, because this is a troubleshooting exercise.

---

## Step 9 — Check DNS

Run:

```powershell
Resolve-DnsName google.com
```

Record whether the DNS query successfully returns an address.

**Evidence:**

PS C:\WINDOWS\system32> Resolve-DnsName google.com

Name                                           Type   TTL   Section    IPAddress
----                                           ----   ---   -------    ---------
google.com                                     AAAA   267   Answer     2607:f8b0:4012:82a::200e
google.com                                     A      267   Answer     192.178.57.46

**Finding:**

<img width="787" height="192" alt="image" src="https://github.com/user-attachments/assets/cd35f2cf-38e3-43c5-9dc3-9ec8b5d1c2e8" />


---

## Step 10 — Identify Resource-Heavy Processes

Run:

```powershell
Get-Process |
Sort-Object CPU -Descending |
Select-Object -First 10 Name, Id, CPU
```

This identifies processes that have accumulated the highest CPU time.

For current memory consumption:

```powershell
Get-Process |
Sort-Object WorkingSet64 -Descending |
Select-Object -First 10 Name, Id,
@{Name="MemoryMB";Expression={[math]::Round($_.WorkingSet64/1MB,2)}}
```

**Evidence:**

<img width="828" height="483" alt="image" src="https://github.com/user-attachments/assets/874f3663-ccbd-466d-978a-1abc89e53cf8" />

<img width="826" height="467" alt="image" src="https://github.com/user-attachments/assets/1f5738b0-c516-4600-b839-a62b7604bb8d" />


Finding — Step 10A: CPU-intensive processes

The CPU-time list is dominated by Microsoft Edge processes:

msedge PID 13528 — 44,483.92 s
msedge PID 7456 — 8,100.41 s
msedge PID 8240 — 8,068.50 s
msedge PID 6684 — 4,253.58 s
Zoom PID 12836 — 2,281.55 s
Other Windows processes such as System, svchost, and dwm also appear.

Important: The CPU value shown by Get-Process is cumulative CPU time used by the process since it started, not its current CPU percentage. Therefore, we cannot conclude from this output alone that Edge is currently consuming 44,483% or even a high percentage of CPU.

Finding: Microsoft Edge has accumulated the highest CPU time among the listed processes, but a current CPU-utilization measurement is still required before identifying it as the cause of the reported performance issue.

Finding — Step 10B: Memory-intensive processes

The highest memory consumers are:

Memory Compression: ~1.65 GB
Microsoft Edge: multiple processes, with the largest at ~646 MB
Other Edge processes: ~536 MB, ~456 MB, ~401 MB, etc.
Windows Explorer: ~291 MB

Finding: Microsoft Edge is using a significant amount of memory across multiple processes, which is normal for a browser with multiple tabs/extensions. However, the most significant individual consumer is Memory Compression at ~1.65 GB.

Combined with Step 5, where approximately 70.9% of physical memory was already in use, the system is showing moderately elevated memory utilization. This could contribute to intermittent performance degradation, particularly on a system with approximately 12 GB of RAM.

However, we cannot yet establish that Edge or Memory Compression is the root cause. We still need to examine Windows services and system events.


---

## Step 11 — Check Important Windows Services

Run:

```powershell
Get-Service |
Where-Object {$_.Status -eq "Stopped"} |
Select-Object Name, DisplayName, Status
```

Review the stopped services.

Do **not** assume that every stopped service is a problem. Many Windows services are intentionally stopped until required.

You can also check specific services when relevant:

```powershell
Get-Service -Name Spooler, wuauserv, Winmgmt
```

**Evidence:**

<img width="806" height="542" alt="image" src="https://github.com/user-attachments/assets/facf178d-bc04-40d7-b6c1-89184a58c144" />


**Finding:**

Finding — Step 11A

The first command shows many Windows services in a Stopped state, but this list by itself does not indicate a problem. Many of these services are designed to start only when their functionality is needed.

For example, wuauserv (Windows Update) being stopped can be normal when Windows Update is not actively performing an operation.

Finding — Step 11B

The three services checked show:

Service	Status	Finding
Spooler	Running	Normal
Winmgmt	Running	Normal
wuauserv	Stopped	Windows Update service is currently inactive

Finding: The Print Spooler and Windows Management Instrumentation (WMI) services are running normally. wuauserv is stopped, but this does not automatically indicate a fault; Windows Update may not need to be running continuously.

No service failure has been established. We should not manually start wuauserv just for this assessment.

---

## Step 12 — Check Windows Event Logs

PowerShell can be used to review recent system errors.

Run:

```powershell
Get-WinEvent -FilterHashtable @{
    LogName='System'
    Level=2
} -MaxEvents 20 |
Select-Object TimeCreated, Id, ProviderName, LevelDisplayName, Message
```

This retrieves recent **System log errors**.

Review the results for recurring:

* Driver problems
* Hardware errors
* Disk errors
* Service failures
* Unexpected shutdowns

**Evidence:**

<img width="830" height="461" alt="image" src="https://github.com/user-attachments/assets/7072320d-f273-4065-b496-be991e932b72" />


**Finding:**

Finding — Step 12

This is a significant finding.

The System event log shows two recurring issues:

Windows Update errors — Event ID 20
Repeated failures with error 0x80073D02
Primarily involving:
MicrosoftWindows.CrossDevice
Microsoft.YourPhone
These errors occurred repeatedly from September 29 through October 3.
Unexpected shutdowns — Event ID 6008
Multiple unexpected shutdown events were recorded on September 29, October 1, October 2, and October 3.

Finding: The workstation has a recurring Windows Update installation problem and multiple unexpected shutdowns recorded in the System event log. These are the first concrete system-level issues identified during the assessment.

However, we cannot yet say that either issue is the cause of the reported intermittent performance problem. We need to correlate them with Windows Update status and installed updates.

Do not modify Windows Update or attempt repairs yet. We're still collecting evidence.

If there are no relevant errors, document that rather than creating one.

---

## Step 13 — Check Windows Update Status

Run:

```powershell
Get-Service wuauserv
```

Then:

```powershell
Get-HotFix |
Sort-Object InstalledOn -Descending |
Select-Object -First 10 HotFixID, InstalledOn, Description
```

This provides information about recently installed Windows updates.

**Evidence:**

<img width="381" height="118" alt="image" src="https://github.com/user-attachments/assets/546ab1db-5292-4deb-928c-1b2bc1f82a44" />

<img width="828" height="180" alt="image" src="https://github.com/user-attachments/assets/49b49588-8d48-4cac-bc4d-00592195840d" />



**Finding:**

Step 13A — Finding

wuauserv is currently:

Status: Stopped

This is consistent with Step 11, so the Windows Update service is not currently running.

However, the Event Viewer evidence shows that Windows Update has repeatedly attempted and failed to install updates with 0x80073D02. Therefore, there is a legitimate Windows Update issue worth documenting.

We still need the second command to see whether the system is receiving/installing recent Windows updates.

Finding — Step 13B

The workstation has several recently installed updates, including:

KB5129195 — Security Update — Sep 19, 2026
KB5124007 — Security Update — Sep 18, 2026
KB5126052 — Update — Sep 18, 2026
Additional updates installed Sep 7, 2026

Finding: The system has successfully installed recent Windows updates, so it is not simply an outdated/unpatched workstation.

However, the Event Viewer shows that Windows Update is also experiencing repeated 0x80073D02 installation failures, specifically involving Microsoft CrossDevice/YourPhone components. Therefore, we have evidence of partial/update-related failures despite successful installation of other updates.

At this point, we should document this as a secondary system issue, not yet the root cause of the performance complaint.

---

## Step 14 — Check System Uptime

Run:

```powershell
(Get-Date) - (Get-CimInstance Win32_OperatingSystem).LastBootUpTime
```

Record the amount of time since the last restart.

**Evidence:**

<img width="687" height="243" alt="image" src="https://github.com/user-attachments/assets/d2e8d6e6-1161-48be-88df-dccaddaad37d" />


**Finding:**

Finding — Step 14

The workstation has been running for approximately:

1 day
3 hours
40 minutes
37 seconds
Total: ~27.68 hours

Finding: The system has been continuously running for a little over 27 hours. This is not an unusually long uptime, so excessive uptime is unlikely to be the primary explanation for the reported performance issue.

However, given the unexpected shutdown events identified in Step 12, the uptime result is useful as supporting evidence for the system's recent operating history.

---

## Step 15 — Generate a Basic System Summary

After collecting the individual results, run:

```powershell
Get-ComputerInfo |
Select-Object CsName, WindowsProductName, WindowsVersion, OsBuildNumber, CsManufacturer, CsModel
```

This provides a concise hardware/software summary.

**Evidence:**

<img width="829" height="174" alt="image" src="https://github.com/user-attachments/assets/d08dc649-43d2-4746-930a-1c8a1e661712" />


**Finding:**

Finding — Step 15

Final system inventory:

Manufacturer: Toshiba
Model: Satellite S45-B
OS: Windows 10 Pro
Version: 2009
Build: 26200
Computer: DESKTOP-Q2MV7OV

Finding: PowerShell successfully identified the workstation hardware and operating-system configuration. The system is an older Toshiba Satellite platform with a 2-core/4-thread Intel i5-4210U and approximately 12 GB RAM.

This hardware profile provides important context for the performance investigation, but it does not by itself establish a hardware failure.

We now have essentially all the diagnostic information. The last step is to perform the final verification so we can determine whether the system is currently stable.

---

<img width="828" height="437" alt="image" src="https://github.com/user-attachments/assets/8764cfb5-31f4-490b-8010-b024e658ccd4" />


Finding — Step 16

The final system information check was successful and matches the earlier inventory:

Computer: DESKTOP-Q2MV7OV
Manufacturer: Toshiba
Model: Satellite S45-B
OS: Windows 10 Pro
Version: 2009
Build: 26200

The CPU performance-counter command failed:

Get-Counter : El objeto especificado no se encontró en el equipo.
CounterApiError

Finding: The requested performance counter was not available through Get-Counter on this workstation, so we cannot use that command as evidence of current CPU utilization. This is a limitation of the diagnostic method, not evidence of a CPU failure.

Overall assessment

We now have enough evidence to close the investigation:

~12 GB RAM, with ~71% utilization during testing.
~384 GB free disk space — healthy.
Network gateway connectivity — successful.
Internet connectivity — successful, with 3 successful replies before a local resource error.
DNS — successful.
Multiple Edge processes and Memory Compression are significant resource consumers.
Spooler and WMI are running normally.
Windows Update is stopped and has repeated 0x80073D02 installation errors.
Multiple Event ID 6008 unexpected shutdowns were recorded.
Uptime ~27.7 hours.
No evidence collected so far establishes a hardware failure.

The strongest findings are the elevated memory usage/resource pressure and the recurring Windows Update/unexpected-shutdown events. We should not claim either one as the definitive root cause without additional evidence.


# Investigation Results

### Workstation

`DESKTOP-Q2MV7OV — Toshiba Satellite S45-B — Windows 10 Pro, Version 2009, Build 26200`

### Current User

`desktop-q2mv7ov\usuario`

The `$env:USERNAME` value also confirmed `Usuario`.

### CPU

`Intel(R) Core(TM) i5-4210U CPU @ 1.70GHz`

* 2 physical cores
* 4 logical processors
* Maximum clock speed: 1.70 GHz

### Memory

`11.91 GB installed`

At the time of assessment:

* Total visible memory: approximately 11.91 GB
* Free physical memory: approximately 3.47 GB
* Approximately 8.44 GB was in use
* Estimated utilization: approximately 70.9%

### Storage

`C: drive — 384.07 GB free of approximately 446.08 GB`

Approximately 86% of the drive capacity was available. No low-disk-space condition was identified.

### Network

The workstation was connected through Wi-Fi using the Qualcomm Atheros AR956x Wireless Network Adapter.

* IPv4 address: `192.168.100.4`
* Default gateway: `192.168.100.1`
* Gateway connectivity: successful, approximately 1 ms
* Internet connectivity: three successful replies to `8.8.8.8`, approximately 16–20 ms
* Fourth test attempt returned a local PowerShell resource error

The available evidence does not indicate a basic network connectivity failure.

### DNS

`Resolve-DnsName google.com` successfully returned both IPv4 and IPv6 records.

DNS resolution was functioning correctly during the assessment.

### Re


# Evidence Folder

```text
08-PowerShell/
└── troubleshooting-cases/
    └── 001-system-health-assessment/
        ├── README.md
        └── evidence/
            ├── 01-system-information.png
            ├── 02-current-user.png
            ├── 03-cpu-information.png
            ├── 04-memory-information.png
            ├── 05-memory-usage.png
            ├── 06-disk-space.png
            ├── 07-network-configuration.png
            ├── 08-network-connectivity.png
            ├── 09-dns-resolution.png
            ├── 10-resource-heavy-processes.png
            ├── 11-windows-services.png
            ├── 12-system-event-errors.png
            ├── 13-windows-update.png
            ├── 14-system-uptime.png
            ├── 15-system-summary.png
            └── 16-final-system-verification.png
```

## Portfolio Skills Demonstrated

This incident demonstrates practical PowerShell usage for:

* Windows system administration
* Hardware/software inventory
* Performance troubleshooting
* Process analysis
* Memory and storage analysis
* Network troubleshooting
* DNS troubleshooting
* Windows service investigation
* Event log analysis
* Windows update investigation
* System uptime analysis
* Service Desk evidence collection
* Technical documentation

