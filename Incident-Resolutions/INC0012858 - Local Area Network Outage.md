# 🎫 Incident Resolution Log: INC0012858

## 🔴 Case Overview & Impact Analysis
*   **Ticket ID:** `INC0012858`
*   **Priority Level:** Critical (Total Floor Outage)
*   **User/Location Affected:** Mike Reeves / 3rd Floor Corporate Office
*   **Business Impact:** Complete loss of internet and local network access for an entire floor. Multiple departments are completely offline, and the customer service team cannot access the critical CRM platform.

---

## 💻 Enterprise Infrastructure & Tooling Architecture
Infrastructure diagnostics and hardware recovery were handled using these systems:
*   **ServiceDesk Simulator ITSM Suite:** Centralized platform utilized to track the critical incident lifecycle, monitor SLA breaches, and manage floor-wide communications.
*   **Cisco Catalyst Managed Access Switching:** The physical Layer 2 infrastructure responsible for distributing localized corporate subnet access to Floor 3 workstations and conference rooms.
*   **On-Premises Main Distribution Frame (MDF):** The physical server room location containing core rack enclosures and power distribution units.

---

## 🔍 Isolation & Diagnostic Workflow
The facilities department reported a sudden, total network blackout affecting all endpoints on the third floor. 

A top-down structural troubleshooting methodology was applied to isolate the fault:
1.  **Horizontal Blast Radius Analysis:** Checked network status for neighboring floors. The second floor was operating normally, isolating the failure strictly to the third-floor hardware distribution plane.
2.  **Logical Layer 3 Checking:** Attempted to ping the Floor 3 gateway. The request timed out repeatedly, indicating the localized routing interface or access switch stack was completely unresponsive.
3.  **Root Cause Determination:** Walked to the physical server room to audit the hardware rack. The managed access switch dedicated to the third floor was in a frozen or unpowered state, causing a total breakdown of Layer 2 data forwarding.

---

## 🛠️ Infrastructure Operations & Resolution
Restoring floor-wide connectivity required direct physical infrastructure intervention within the server room environment.

### 1. Hardware State Triage
Located the specific frozen 3rd-floor access switch inside the infrastructure rack enclosure. Visual inspection showed anomalous diagnostic light patterns, confirming the operating system kernel had locked up.

### 2. Hard Power Cycle Execution
Executed a controlled physical power cycle. Disconnected the power input cables from the power distribution unit, waited 30 seconds to allow internal circuit components to fully de-energize, and re-seated the power lines.

### 3. Initialization Verification
Monitored the hardware boot sequence. The switch completed its POST (Power-On Self-Test) routines, re-loaded its startup configuration parameters from NVRAM, and brought all connected ethernet interfaces back into an active link state.

---

## 📊 Post-Incident Metrics & Status
*   **Affected Subnet Domain:** Floor 3 LAN Access Plane
*   **User Verification:** Confirmed that local workstations successfully re-acquired DHCP configurations. Internet access was fully restored floor-wide, and the customer service team re-established active CRM sessions.
*   **Final Ticket Status:** Closed / Resolved
*   <img width="1837" height="628" alt="image" src="https://github.com/user-attachments/assets/a890b216-aa16-44d4-a5b2-86f3f9991358" />
