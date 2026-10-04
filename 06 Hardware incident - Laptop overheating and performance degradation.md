# Hardware Incident 001 — Laptop Overheating and Performance Degradation

## Issue

User reports that the Windows laptop becomes unusually hot during normal use. The cooling fan runs continuously or at high speed, and the system becomes noticeably slower when performing routine tasks.

## Initial Symptom

The user reports increased system temperature, persistent fan activity, and reduced performance. The issue appears to affect general system responsiveness rather than a single application.

**Affected device:**
Single Windows workstation / laptop.

---

## Investigation

### Step 1 — Review system resource utilization

Open **Task Manager → Performance** and review:

* CPU utilization
* Memory utilization
* Disk utilization
* GPU utilization

The system should be observed while idle before opening additional applications.

**Evidence:**

<img width="652" height="292" alt="image" src="https://github.com/user-attachments/assets/de2e65a4-d418-4bc0-89f4-7e03b54e6834" />


---

### Step 2 — Identify processes consuming excessive resources

Open:

**Task Manager → Processes**

Sort by:

* CPU
* Memory
* Disk

Identify whether a specific application or background process is consuming an unusually large amount of system resources.

Do not terminate a process unless its purpose is understood and stopping it is appropriate.

**Evidence:**
<img width="651" height="276" alt="image" src="https://github.com/user-attachments/assets/20825ce8-1ecc-4388-9407-47b34bb63901" />


---

### Step 3 — Check system uptime and recent restart

Open:

**Task Manager → Performance → CPU**

Review **Up time**.

A very long uptime can help explain accumulated resource usage or pending system maintenance, although it does not by itself establish the root cause.

**Evidence:**
<img width="803" height="537" alt="image" src="https://github.com/user-attachments/assets/b3e193d7-0b72-4a6a-8bb6-e4c8f5dc85b5" />


---

### Step 4 — Check Windows Update status

Open:

**Settings → Windows Update**

Verify whether Windows is:

* Fully updated
* Downloading updates
* Installing updates
* Waiting for a restart
* Reporting an update error

Updates can temporarily increase CPU, disk, and fan activity.

**Evidence:**
<img width="504" height="574" alt="image" src="https://github.com/user-attachments/assets/d2809098-c632-41d6-afb4-70faca9797b6" />


---

### Step 5 — Check available storage

Open:

**File Explorer → This PC**

Review the available space on the system drive.

Low disk space can contribute to poor system performance and may interfere with Windows maintenance activities.

**Evidence:**
<img width="574" height="494" alt="image" src="https://github.com/user-attachments/assets/b46e00da-c67a-4df9-915e-fe0736740e52" />


---

### Step 6 — Check for hardware-related warnings

Open:

**Event Viewer → Windows Logs → System**

Review recent warnings and errors related to:

* Hardware
* Thermal events
* Disk
* Drivers
* Unexpected shutdowns
* Device failures

Do not assume every warning is related to the reported issue. Correlate the event time with the user's symptoms.

**Evidence:**
<img width="588" height="291" alt="image" src="https://github.com/user-attachments/assets/07ffe419-537a-4116-b459-adb7d9089283" />

---

### Step 7 — Check Device Manager

Open:

**Device Manager**

Review the hardware categories for warning icons or devices reporting problems.

Pay particular attention to:

* Display adapters
* Network adapters
* Storage controllers
* Processors
* System devices

**Evidence:**

<img width="977" height="704" alt="image" src="https://github.com/user-attachments/assets/ea8b313b-08b0-403f-b0bb-7446aee881c8" />


---

### Step 8 — Check system temperature / thermal information

If the workstation provides accessible temperature information through the manufacturer's hardware utility or BIOS/UEFI hardware diagnostics, review the available readings.

**Evidence:**
<img width="474" height="344" alt="image" src="https://github.com/user-attachments/assets/e1f8ef59-f05b-4aee-a06e-a2a1fef1ab63" />


**Lab limitation if applicable:**
`[Temperature telemetry was not available through the standard Windows tools used during this investigation.]`

---

### Step 9 — Perform physical inspection

If the device can be safely inspected, check:

* Air vents
* Fan openings
* Dust accumulation
* Obstructions around ventilation
* Physical damage
* Unusual fan noise

Do not open the laptop or remove internal components unless authorized and appropriate for the device.

**Evidence:**
<img width="662" height="438" alt="image" src="https://github.com/user-attachments/assets/170e426d-7fbb-41ce-acff-8ce997b2b908" />


---

### Step 10 — Controlled restart and verification

Restart the workstation and allow Windows to load completely.

After startup, allow the system to remain idle for several minutes and then review Task Manager again.

Compare the system behavior with the initial observation.

**Evidence:**

<img width="1356" height="903" alt="image" src="https://github.com/user-attachments/assets/28752991-3c05-46f2-baac-478975a3c7f3" />


---

# Investigation Results

**System resource utilization:**
Initial Task Manager review showed approximately **50% CPU utilization** and **76% memory utilization**. System resource usage was elevated during the initial investigation, particularly memory utilization.

**Resource-consuming process:**
Running processes were reviewed in Task Manager to identify applications or background processes contributing to the elevated resource utilization. No specific process was identified as a confirmed hardware fault based on the available evidence.

**System uptime:**
The workstation had been running for approximately **18 hours, 51 minutes, and 54 seconds** before the restart. This was not considered unusually long and was not identified as a significant contributing factor to the reported performance issue.

**Windows Update status:**
Windows Update was reviewed and showed that **no system updates were required**. No pending update activity or required restart related to Windows Update was identified.

**Available storage:**
The system drive had approximately **386 GB available out of 446 GB total capacity**, leaving approximately **60 GB in use**. Available storage was considered sufficient and was not identified as a likely cause of the reported performance issue.

**Hardware/System events:**
Windows Event Viewer was reviewed for recent hardware, disk, driver, thermal, and other system-related errors or warnings. **No relevant events were identified** during the investigation.

**Device Manager status:**
Device Manager was reviewed for hardware or driver problems. **No warning indicators or hardware alerts were present.**

**Thermal information:**
The CPU temperature was approximately **28°C (82°F)**. Overall system temperature was approximately **65°C (149°F)**. The readings did not indicate an immediate thermal emergency during the investigation.

**Physical inspection:**
The workstation was physically inspected. **No visible dust accumulation, ventilation obstruction, or physical damage was identified.**

**Post-restart behavior:**
Following a system restart, CPU utilization decreased significantly from approximately **50% to 2%**. This substantial reduction in CPU activity indicated that the elevated CPU usage was transient rather than evidence of a persistent hardware failure.



---

# Root Cause

No hardware fault was reproduced during troubleshooting.

The workstation initially showed approximately **50% CPU utilization and 76% memory utilization**, but there were no relevant hardware or system events in Event Viewer, no hardware warnings in Device Manager, no visible physical damage or ventilation obstruction, and the recorded CPU temperature was only **28°C (82°F)**.

Available storage was also sufficient, with **386 GB available out of 446 GB**. Windows Update reported that no updates were required.

Following a system restart, CPU utilization dropped from approximately **50% to 2%**. Based on the available evidence, the reported performance issue was most consistent with **transient system resource utilization rather than a persistent hardware or thermal failure**.

A specific resource-consuming process could not be established as the definitive cause.

---

# Resolution

The workstation was **restarted** as part of the troubleshooting process.

Following the restart, system resource utilization was reassessed and CPU usage decreased substantially from approximately **50% to 2%**.

No hardware components were replaced, no drivers were modified, no physical repair was required, and no ventilation obstruction was identified.

The issue was considered resolved after the system returned to normal CPU utilization following the restart.

---

# Verification

**CPU utilization after resolution:**
CPU utilization decreased to approximately **2%** after the restart.

**Memory utilization after resolution:**
Memory utilization was not recorded after the restart and therefore no specific post-resolution percentage is being claimed.

**Fan behavior:**
No persistent abnormal fan behavior or thermal condition was identified during the investigation.
**Result:** No hardware-related fan fault was reproduced.

**System responsiveness:**
The workstation was reassessed after the restart. The significant reduction in CPU utilization indicated that the elevated system load had cleared.
**Result:** System performance was considered improved following the restart.

**Hardware warnings:**
No hardware warning indicators were present in Device Manager, and no relevant hardware/system errors were identified in Event Viewer.

**Post-restart behavior:**
After restarting the workstation, CPU utilization decreased from approximately **50% to 2%**. No persistent hardware or thermal fault was reproduced.

**User confirmation:**
The user confirmed that the reported performance issue was resolved after the workstation restart.

---

# Final Ticket Notes

The workstation was investigated following the user's report of increased heat, persistent fan activity, and reduced system performance. System resource utilization, active processes, system uptime, Windows Update status, available storage, Windows hardware-related events, Device Manager, available thermal information, and physical hardware condition were reviewed.

The investigation findings were compared against the reported symptoms to determine whether the issue was caused by excessive system resource usage, Windows activity, a driver/device problem, thermal conditions, physical ventilation, or another hardware-related condition.

Following the corrective action, the workstation was restarted and system behavior was reassessed. Final verification was performed to confirm whether the reported symptoms persisted.

**Final status:**
`[Resolved ]`

---

# Evidence Folder

```text
06-Hardware/
└── troubleshooting-cases/
    └── 001-laptop-overheating-performance/
        ├── README.md
        └── evidence/
            ├── 01-task-manager-performance.png
            ├── 02-resource-consuming-process.png
            ├── 03-system-uptime.png
            ├── 04-windows-update-status.png
            ├── 05-storage-capacity.png
            ├── 06-hardware-system-event.png
            ├── 07-device-manager.png
            ├── 08-thermal-information.png
            ├── 09-physical-hardware-inspection.png
            ├── 10-post-restart-verification.png
            └── 11-final-hardware-verification.png
