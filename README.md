# Active Directory Home Lab: Enterprise Network Deployment

## 1. Project Overview & Objectives
This project demonstrates the setup of an isolated corporate network infrastructure within a virtualized environment. The core goal of this lab is to understand user identity management, network segmentation, centralized authentication, and core IT operations. By deploying a Windows Server 2022 Domain Controller alongside a Windows 10 Client, I simulated a standard corporate directory environment from scratch.

### Key Skills Demonstrated:
* **Virtualization Management:** Creating and configuring isolated internal virtual switches.
* **Network Infrastructure:** Assigning static IPv4 schemas and manual DNS pointings.
* **Centralized Identity Management:** Provisioning Active Directory Domain Services (AD DS).
* **System Administration:** Structuring corporate hierarchies with OUs, Security Groups, and User Lifecycle Management.

---

## 2. Network Topology & Architecture
To ensure safety and security, the entire infrastructure runs inside a closed private broadcast domain disconnected from the physical host's network.

* **Hypervisor Platform:** Oracle VM VirtualBox
* **Virtual Network Switch:** `LabNetwork` (Internal Network mode)
* **Domain Controller (`Lab-DomainController`):** * Operating System: Windows Server 2022 Datacenter
  * IP Address: `192.168.10.1`
  * Subnet Mask: `255.255.255.0`
  * Active Roles: AD DS, DNS Server
* **Client Workstation (`Lab-Windows10`):**
  * Operating System: Windows 10 Enterprise
  * IP Address: `192.168.10.10`
  * Subnet Mask: `255.255.255.0`
  * Preferred DNS Server: `192.168.10.1`

---

## 3. Implementation Steps

### Phase 1: Core Networking & Server Setup
1. Isolated both virtual machines by switching their network adapters from NAT to **Internal Network** with the identifier `LabNetwork`.
2. Statically assigned the server's IP address to `192.168.10.1` via the network adapter properties GUI (ncpa.cpl).
3. Successfully installed and verified the active directory domain service roles on the server manager platform.

<img width="959" height="566" alt="Screenshot 2026-06-29 201314" src="https://github.com/user-attachments/assets/2e80e4bb-a9f2-4070-a48a-c20bec12d017" />
<img width="479" height="563" alt="Screenshot 2026-06-29 200144" src="https://github.com/user-attachments/assets/c4406971-7761-457a-bf19-31a689239817" />

### Phase 2: Active Directory Directory Architecture
1. Constructed a corporate organizational hierarchy by creating a parent Organizational Unit (OU) called **Corporate Office**.
2. Built departmental sub-OUs for **Finance**, **HR**, **IT Department**, and **Marketing** to mimic standard corporate organizational patterns.
3. Created a global security group called **HelpDesk_L1** within the IT department folder to manage permissions dynamically.
4. Created a centralized domain user profile for **John Doe** (`jdoe`) and nested his identity inside the HelpDesk security group to inherit team permissions.

<img width="959" height="565" alt="Screenshot 2026-06-29 200622" src="https://github.com/user-attachments/assets/48745468-b7b0-4898-9028-ded8370dc8d6" />
<img width="959" height="565" alt="Screenshot 2026-06-29 200513" src="https://github.com/user-attachments/assets/bd84b8b4-963c-4b4c-ae01-99712255ac82" />


### Phase 3: Client Integration & Verification
1. Logged into the Windows 10 desktop environment and pointed the computer's Preferred DNS Server directly to the Domain Controller's IP (`192.168.10.1`).
2. Dispatched an ICMP packet request (`ping`) from the client to the server to verify complete internal connectivity.
3. Formally changed the workstation system properties from a workgroup system to a member of the `corporate.local` domain.
4. Authenticated against the active directory database at startup to verify successful network profile setup.

<img width="479" height="562" alt="Screenshot 2026-06-29 200107" src="https://github.com/user-attachments/assets/d4bebd4a-cc68-4e48-bccb-d96a1c100746" />


---

 Operational Troubleshooting & Lessons Learned
* **The DNS Dependency:** During initial configuration, attempts to reach the domain controller by name failed. I observed that windows operating systems rely strictly on DNS to resolve the location of a domain controller. Manually overriding the automatic adapter setting to specify `192.168.10.1` as the primary DNS lookup mechanism instantly solved the issue.
* **Centralization Mechanics:** This exercise effectively demonstrates how enterprise infrastructures handle scale. By using security groups instead of configuring individual computers manually, IT help desk technicians can immediately authorize or restrict network capabilities for thousands of endpoints natively through the Domain Controller.
* 
## Phase 4: Installing the Help Desk Software (osTicket & XAMPP)

To make this lab feel like a real IT job, I needed a way for users to submit help requests. I decided to install an open-source program called **osTicket** directly onto my Windows Server. Since real companies don't just run software out of a basic folder, I had to set up a full local web server environment to host it.

### The Tools Used:
* **XAMPP:** A bundle package that gave me a local web server (**Apache**) and a database database container (**MySQL**).
* **osTicket:** The actual software my "users" and "IT agents" will interact with.

### Exactly How I Set It Up:
1. **Moved the Files:** I dropped the osTicket files right into the server's web directory (`C:\xampp\htdocs\osticket`) so the Apache web server could read them.
2. **Fixed Server Settings:** Out of the box, XAMPP turns off features osTicket needs. I went into the server's backend configuration file (`php.ini`) using Notepad and manually turned on the extensions for time zones (`intl`), graphics handling (`gd`), and email routing (`imap`). 
3. **Created the Database:** I opened up the database controller (phpMyAdmin) and created a blank database room called `osticket` so the app would have a place to save user tickets, passwords, and logs.
4. **Locked Down Security:** After running the installer successfully, I renamed the master config file to `ost-config.php`, flipped its windows properties to **Read-Only** so it couldn't be tampered with, and completely deleted the setup folder so nobody could reset my application from the outside.
<img width="959" height="563" alt="Screenshot 2026-06-30 194523" src="https://github.com/user-attachments/assets/e0c72f11-3a15-4aff-8020-b50a75b82f26" />
<img width="959" height="566" alt="Screenshot 2026-06-30 193813" src="https://github.com/user-attachments/assets/b9407d31-d8ac-4c89-bbeb-6bc88a292e61" />
### 📁 Project Phase: Help Desk Simulation & Identity Management

### 🛠️ Overview
This phase simulates an enterprise IT environment by integrating user-facing help desk operations with system administration. Using **osTicket** as the central ticketing system and **Active Directory (AD DC)** for identity management, I acted as both the end-user reporting technical issues and the IT Support Engineer resolving them through account provisioning, security policy enforcement, and permission escalation.

---

### 💻 System Architecture & Setup Choices (Why This Matters)
*   **Virtual Network Isolation:** The environment is configured using an **Internal Network** within VirtualBox. This isolates the Domain Controller and Client machines from the physical local network, establishing a safe sandbox for system modifications without security risks to external production environments.
*   **Static IP Framework:** The Domain Controller is assigned a manually configured static IP address. In enterprise networking, infrastructure servers must retain a constant IP address to ensure reliable DNS resolution and prevent communication failures with client workstations.

---

### 🚀 Lab Simulations & Ticket Resolutions

#### 🔹 Case 1: Employee Onboarding & Account Provisioning
*   **Scenario:** HR submitted a ticket requesting a corporate network account for a new Marketing hire, John Doe.
*   **Technical Resolution:** 
    1. Logged into the `osTicket Staff Panel`, claimed the ticket, and moved it to an active status.
    2. Opened **Active Directory Users and Computers (ADUC)** on the Windows Server Domain Controller.
    3. Verified the corporate hierarchy and ensured a proper **Organizational Unit (OU)** existed for the `Marketing` department to allow targeted Group Policy deployment.
    4. Created a new user object (`jdoe`) within the Marketing OU.
    5. Configured security best practices by assigning a temporary password and enforcing **"User must change password at next logon."** This ensures administrative compliance with data privacy standards, as the engineer never learns the user's permanent private credentials.
    6. Logged the technical closure notes in osTicket and marked the ticket as **Resolved**.
#### 📸 Deployment Screenshots

<img width="959" height="562" alt="Screenshot 2026-07-01 210847" src="https://github.com/user-attachments/assets/73c812c9-e045-43b4-91e5-ea54c2dc65c6" />
<img width="959" height="565" alt="Screenshot 2026-07-01 210702" src="https://github.com/user-attachments/assets/6d008986-a31f-4346-9502-dedb61d45650" />

#### 🔹 Case 2: Account Lockout Remediation
*   **Scenario:** A Finance department accountant reported being locked out of their workstation after multiple failed login attempts following a vacation.
*   **Technical Resolution:**
    1. Located the urgent security ticket in the osTicket queue and assigned it to my administrative profile.
    2. Accessed **ADUC**, navigated to the `Finance` OU, and opened the properties for user `dmiller`.
    3. Under the **Account** tab, identified that the account was flagged as locked by the domain's security policies.
    4. Selected the **"Unlock account"** checkbox and applied the changes to restore immediate access.
    5. Provided a professional technical response to the user via osTicket explaining the lockout mechanism, advised careful credential entry to avoid re-triggering the security threshold, and closed the ticket.

<img width="959" height="560" alt="Screenshot 2026-07-01 211049" src="https://github.com/user-attachments/assets/9dbb25d5-a366-41a9-9253-80895e07ed21" />
<img width="959" height="564" alt="Screenshot 2026-07-01 210943" src="https://github.com/user-attachments/assets/e5af74e8-f84a-42a6-97e0-52b03c502680" />
<img width="959" height="564" alt="Screenshot 2026-07-01 210817" src="https://github.com/user-attachments/assets/9fe426b9-c1e7-4b4b-b314-0bab0b4338ef" />
<img width="959" height="563" alt="Screenshot 2026-07-01 210742" src="https://github.com/user-attachments/assets/13f37a9e-19de-452a-a0a3-5147efb09800" />

#### 🔹 Case 3: Role Escalation & Security Group Membership
*   **Scenario:** A newly promoted IT Operations supervisor requested access to restricted Tier 2 internal documentation folders that were throwing permission errors.
*   **Technical Resolution:**
    1. Opened the ticket in osTicket and initialized ownership to track the administrative escalation.
    2. Opened **ADUC** to manage the user's domain security token.
    3. Modified the user's account properties by navigating to the **Member Of** tab.
    4. Added the user to the higher-privileged security group (e.g., `Domain Admins` / `HelpDesk_L2`) to grant inherited read/write permissions for the network file share.
    5. Informed the user via the help desk platform that the permissions were active, and advised a local workstation logoff/logon cycle to regenerate their Kerberos security token with the new group memberships. Closed the ticket.
#### 📸 Deployment Screenshots
<img width="959" height="564" alt="Screenshot 2026-07-01 210943" src="https://github.com/user-attachments/assets/9d84c9f3-83e6-4a6e-84c5-36346b9032f9" />
<img width="959" height="564" alt="Screenshot 2026-07-01 210817" src="https://github.com/user-attachments/assets/f6b40647-6ab3-4e47-b443-9ab7d795b17f" />

---

### 🔑 Key Portfolio Takeaways
*   **User Lifecycle Management:** Hands-on experience with user account creation, security group assignment, and account lockout management inside a Windows Server environment.
*   **Ticketing Proficiency:** Complete mastery of the ticket lifecycle (Creation ➡️ Triage ➡️ Assignment ➡️ Resolution ➡️ Documentation).
*   **Enterprise Best Practices:** Demonstrated understanding of data privacy (enforced password resets) and role-based access control (RBAC via security groups).
