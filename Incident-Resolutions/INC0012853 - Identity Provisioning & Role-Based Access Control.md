# 🎫 Incident Resolution Log: INC0012853

## 🔴 Case Overview & Impact Analysis
* **Ticket ID:** `INC0012853`
* **Priority Level:** Medium
* **User Affected:** Jennifer Torres (Junior Developer)
* **Business Impact:** New employee onboarding setup. HR requested her account and permissions be fully configured before Monday orientation at 9:00 AM so she can start working right away.

---

## 💻 Software Used
* **ServiceDesk Simulator:** Used to view the HR onboarding request and manage the ticket status.
* **Active Directory (AD Tool):** Used to check user details and configure security group memberships.

---

## 🔍 Onboarding Requirements
HR provided the necessary info to create and set up the new developer profile:
1.  **User Details:** Name: Jennifer Torres, Username: `jtorres`, Manager: Tom Wilson, Employee ID: `EMP-4008`.
2.  **Access Rules:** Per security policy, she only gets access groups required for her specific role to avoid privilege creep.
3.  **Requested Access:** The ticket specified she needs the Engineering group, VPN access for remote work, and code repository access.

---

## 🛠️ Resolution

### 1. Verify User Profile Info
I opened the Active Directory tool and pulled up Jennifer's profile to double-check that her display name, department (`Engineering`), employee ID, and manager details matched the HR request form exactly.

### 2. Configure Security Group Memberships
I switched over to the **Groups** tab in the directory utility to assign her permissions. I manually added her profile to the three requested groups:
* `Engineering` (For local department file shares)
* `VPN-Users` (For secure remote network connections)
* `CodeRepo-Access` (For corporate code repository permissions)

### 3. Confirm Baseline Access
I verified the changes took effect. Her account successfully shows active membership in the three requested security groups alongside the standard corporate `Domain Users` baseline.

---

## 📊 Status
* **Fulfillment Verification:** Account created and all requested permissions mapped properly. The profile is ready for her first day on Monday.
* **Final Ticket Status:** Closed / Resolved

<img width="914" height="493" alt="Screenshot 2026-07-11 164936" src="https://github.com/user-attachments/assets/30a50f9f-b8e4-4231-9903-353c2e17f4e1" />
<img width="906" height="464" alt="Screenshot 2026-07-11 165136" src="https://github.com/user-attachments/assets/84eee5ec-c434-478d-9a01-425438501b48" />
<img width="908" height="494" alt="Screenshot 2026-07-11 164945" src="https://github.com/user-attachments/assets/8713bb39-7b62-4899-bcaa-455840e9c336" />
