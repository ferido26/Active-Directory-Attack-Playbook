# Active Directory Red Team Lab (CRTP Style)

## 👨‍💻 Author
Ferido Fernando  
📧 feridofdo26@gmail.com  

---

## 🎯 Objective
This project simulates a real-world **Active Directory attack** starting from a low-privileged user and achieving **Domain Dominance**.

The goal was to:
- Perform domain enumeration
- Escalate privileges
- Move laterally across systems
- Exploit misconfigurations
- Compromise Domain Controller

---

## 🏢 Environment
- Windows Active Directory Lab
- Multiple domain-joined machines
- Tools used in real-world red teaming

---

## ⚙️ Tools Used
- PowerView
- BloodHound / SharpHound
- Mimikatz / SafetyKatz
- Rubeus
- Certify
- WinRS / PowerShell Remoting

---

## 🔍 Attack Chain Overview

### 1. Initial Access (STDVM)
- Enumerated domain using PowerView
- Identified users, computers, and groups

---

### 2. Local Privilege Escalation
- Discovered credentials in shared folder
- Used `runas` to gain admin access
- Added user to Administrators group

---

### 3. Credential Dumping
- Disabled Defender protections
- Extracted credentials using Mimikatz
- Retrieved AES keys for machine accounts

---

### 4. Lateral Movement (MGMTSRV)
- Used Rubeus to request TGT
- Verified with `klist`
- Gained access using WinRS

---

### 5. RBCD Abuse
- Exploited GenericWrite permissions
- Configured Resource-Based Constrained Delegation
- Impersonated privileged user (techadmin)

---

### 6. Privilege Escalation via Groups
- Abused AddSelf permissions
- Added user to Management group
- Reset password of privileged account

---

### 7. Remote Execution (TECHSRV30 & ADMINSRV86)
- Established PowerShell remoting
- Dumped credentials again
- Identified active user sessions

---

### 8. ADCS Misconfiguration (ESC3)
- Found vulnerable certificate templates
- Used Certify to request certificates
- Impersonated techadmin using certificates

---

### 9. Domain Controller Compromise
- Accessed Domain Controller via WinRS
- Performed DCSync attack
- Extracted krbtgt hash

---

### 10. Cross-Domain Attack
- Forged Silver Ticket using trust key
- Attempted access to finance domain

---

## ⚠️ What Went Wrong
- Incorrect service selection during Silver Ticket attack
- Could not access SMB share due to wrong service (HTTP instead of CIFS)

---

## 🛡️ Key Learnings
- Misconfigurations in AD can lead to full domain compromise
- Credential exposure is a major risk
- Delegation and ADCS are powerful attack vectors
- Proper enumeration is critical

---

## 🔐 Security Recommendations
- Restrict access to shared folders
- Use secure credential storage
- Implement AppLocker / WDAC
- Monitor PowerShell activity
- Fix ADCS misconfigurations
- Apply least privilege principle

---

## 📂 Project Structure
