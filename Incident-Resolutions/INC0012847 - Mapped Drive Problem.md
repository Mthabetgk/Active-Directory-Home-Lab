# 🎫 Incident Resolution Log: INC0012847

## 🔴 Case Overview & Impact Analysis
* **Ticket ID:** `INC0012847`
* **Priority Level:** High
* **User Affected:** Sarah Mitchell (Marketing Department)
* **Business Impact:** Sarah is working from home and can't get into the Marketing shared drive. She has a deadline tomorrow for Q1 campaign materials, so she needs access back immediately.

---

## 💻 Software Used
* **ServiceDesk Simulator:** Used to handle the user chat and manage the ticket lifecycle.
* **VPN Client:** Used to connect Sarah's remote laptop back to the company network.
* **Windows File Explorer:** Used to manually map the network drive path.

---

## 🔍 Troubleshooting Steps
Sarah reported getting a "The network path was not found" error when trying to open her files. 
1.  **Check Internet Connection:** I verified her internet and email were working fine, so it wasn't a local Wi-Fi drop.
2.  **Check Drive Status:** Her mapped drives showed a disconnected status because she was working from home and wasn't on the corporate network yet.
3.  **Find the Cause:** She didn't have her VPN turned on. Without the VPN, her computer can't reach the internal file server (`FILESERV01`).

---

## 🛠️ Resolution
I looked up the correct drive mapping path in the internal documentation and walked Sarah through fixing it.

### 1. Connect to the VPN
I told Sarah to open her VPN client and connect. Turning this on established the connection from her home network to the corporate servers.

### 2. Map the Network Drive
Once the VPN was connected, I went into File Explorer on her machine to manually re-add the missing share:
* **Drive Letter:** `D:`
* **Folder Path:** `\\FILESERV01\departments\Marketing`

I hit finish, and the network drive mounted successfully without throwing any path errors.

---

## 📊 Status
* **User Verification:** Sarah checked her file explorer, confirmed she could see the files again, and closed out the chat.
* **Final Ticket Status:** Closed / Resolved
