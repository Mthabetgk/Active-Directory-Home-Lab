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
