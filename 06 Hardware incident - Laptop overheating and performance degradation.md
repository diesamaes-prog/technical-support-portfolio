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
`10-post-restart-verification.png`

**[INSERT EVIDENCE HERE]**

---

# Investigation Results

**System resource utilization:**
[RESULT]

**Resource-consuming process:**
[RESULT]

**System uptime:**
[RESULT]

**Windows Update status:**
[RESULT]

**Available storage:**
[RESULT]

**Hardware/System events:**
[RESULT]

**Device Manager status:**
[RESULT]

**Thermal information:**
[RESULT]

**Physical inspection:**
[RESULT]

**Post-restart behavior:**
[RESULT]

---

# Root Cause

[COMPLETE AFTER INVESTIGATION]

The root cause should be based on the evidence collected.

Do not automatically state that the laptop is overheating because the fan is loud. Likewise, do not automatically blame dust, thermal paste, CPU usage, or a hardware failure without supporting evidence.

Possible evidence-supported conclusions could include:

* Excessive CPU usage caused by a specific process
* Background Windows activity temporarily increasing system load
* Insufficient available storage contributing to degraded performance
* Hardware/driver issue identified through Event Viewer or Device Manager
* Thermal issue supported by available temperature information
* Physical ventilation obstruction
* No hardware fault reproduced during troubleshooting
* Issue requires hardware repair/escalation

---

# Resolution

[COMPLETE AFTER INVESTIGATION]

Document the **actual action taken**.

Examples:

* High-resource application/process identified and corrected
* Windows update completed and system restarted
* Unnecessary application closed
* Storage issue addressed
* Hardware driver issue corrected
* Ventilation obstruction removed
* Device referred for hardware service
* No fault reproduced; monitoring recommended
* Escalated to hardware support

---

# Verification

**CPU utilization after resolution:**
[RESULT]

**Memory utilization after resolution:**
[RESULT]

**Fan behavior:**
[RESULT]

**System responsiveness:**
[RESULT]

**Hardware warnings:**
[RESULT]

**Post-restart behavior:**
[RESULT]

**User confirmation:**
[RESULT]

**Evidence:**
`11-final-hardware-verification.png`

**[INSERT EVIDENCE HERE]**

---

# Final Ticket Notes

The workstation was investigated following the user's report of increased heat, persistent fan activity, and reduced system performance. System resource utilization, active processes, system uptime, Windows Update status, available storage, Windows hardware-related events, Device Manager, available thermal information, and physical hardware condition were reviewed.

The investigation findings were compared against the reported symptoms to determine whether the issue was caused by excessive system resource usage, Windows activity, a driver/device problem, thermal conditions, physical ventilation, or another hardware-related condition.

Following the corrective action, the workstation was restarted and system behavior was reassessed. Final verification was performed to confirm whether the reported symptoms persisted.

**Final status:**
`[Resolved / Monitoring / Escalated]`

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
```

**Important:** only put screenshots/results that you actually obtained. If a temperature reading, hardware event, or fault isn't available on your machine, document it as **not available/not reproduced** rather than fabricating evidence.

