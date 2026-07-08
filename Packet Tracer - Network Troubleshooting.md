
### 🌐 Cisco Core Infrastructure & Dynamic Identity Architecture

### 🛠️ Topology Overview
I engineered a localized corporate network environment utilizing Cisco Packet Tracer to establish physical and logical connectivity baselines for enterprise network services. The physical design anchors an edge router to a 24-port managed access switch, provisioning dedicated links for corporate infrastructure servers and client workstations.

<img width="957" height="564" alt="Screenshot 2026-07-04 162412" src="https://github.com/user-attachments/assets/4af90c6a-4964-4b4b-a474-4f1392525b0c" />
---

### ⚙️ Implemented Configurations & Rationale

#### 1. Authoritative Gateway Routing
* **Configuration:** Bound static IP gateway properties (`192.168.10.1/24`) to the core router interface using the Cisco IOS Command Line Interface.
* **Technical Rationale:** Establishing an explicit default gateway layer ensures all internal local access network traffic possesses a deterministic exit pathway when attempting to communicate with external subnets or public web services.

#### 2. Automated Network Provisioning (DHCP Integration)
* **Configuration:** Initialized and bound the DHCP service daemon onto the Active Directory Domain Controller (`192.168.10.2`). Defined a controlled distribution scope starting at host parameter `.10` through `.60`.
* **Technical Rationale:** Centralizing the dynamic allocation process ensures all workstation endpoints automatically pull correct IP configurations upon link initialization. By embedding the DNS option parameter to target the Domain Controller's static IP directly, client workstations are programmatically configured to perform seamless Active Directory domain record lookups.

#### 3. Administrative Switch Hardening
* **Configuration:** Executed access restriction profiles via the Cisco IOS CLI on the managed switch infrastructure:
  * Modified the local execution state boundary using cryptographically secure `enable secret` primitives.
  * Explicitly configured `transport input ssh` across all Virtual Terminal Line interfaces (`vty 0 15`), while fully deprecating cleartext Telnet options.
* **Technical Rationale:** Out-of-the-box networking hardware transmits administrative management plane details in unencrypted clear text. Forcing SSH transport structures guarantees that any remote configurations are cryptographically scrambled, protecting administrative credentials from local network packet sniffing or man-in-the-middle exploits.

<img width="680" height="381" alt="Screenshot 2026-07-04 162547" src="https://github.com/user-attachments/assets/cc6f7789-faff-4567-a563-7401bb40b54d" />
<img width="673" height="280" alt="Screenshot 2026-07-04 162428" src="https://github.com/user-attachments/assets/1f08afd1-3325-41b4-ac9f-1102b888bd97" />
