# 🛡️ Active Directory Hardening – SOC / Blue Team Notes

## 📌 Overview

Active Directory (AD) is the core identity and access management system in most enterprise environments. Since AD controls authentication, authorization, and privilege assignment, it is a primary target for attackers during internal compromise and lateral movement.

This room focuses on hardening AD using defensive best practices aligned with SOC monitoring, detection engineering, and incident response readiness.

---

## 🎯 Core Hardening Areas

- Secure authentication mechanisms
- Host and domain hardening via GPO
- Least Privilege & tiered administration
- Detection & mitigation of common AD attacks
- Post-compromise recovery planning

---

# 🔐 1️⃣ Secure Authentication (Defensive Focus)

### Enforce Strong Identity Controls
- Minimum password length & complexity
- Account lockout thresholds
- Password history enforcement
- Multi-Factor Authentication (MFA) for privileged accounts

### Disable Weak Protocols
- Disable NTLM (where possible)
- Enforce Kerberos (AES encryption)
- Disable SMBv1
- Disable LLMNR & NetBIOS to prevent poisoning attacks

### Secure Service & Privileged Accounts
- Use gMSA (Group Managed Service Accounts)
- No interactive logon for service accounts
- Rotate privileged credentials regularly
- Separate admin and standard user accounts

### SOC Monitoring Focus
Monitor:
- Event ID 4624 (Successful logon)
- Event ID 4625 (Failed logon)
- Event ID 4768 / 4769 (Kerberos TGT / TGS requests)
- Unusual authentication times or source systems
- Excessive ticket requests (possible Kerberoasting)

---

# 🖥️ 2️⃣ Host & Domain Hardening via GPO

Group Policy is a central defensive control mechanism in AD.

### Security Hardening via GPO
- Enforce password & lockout policies
- Enable advanced audit policies
- Restrict local administrator access
- Configure Windows Defender & Firewall
- Disable unnecessary services
- Enforce secure RDP configuration
- Block USB storage (if required)
- Enforce automatic updates

### Logging & Auditing Configuration
Enable:
- Logon/Logoff auditing
- Account management auditing
- Directory service access auditing
- Privilege use auditing
- Object access auditing

Forward logs to:
- SIEM (Splunk, Sentinel, ELK, etc.)
- Central log collectors

---

# 👤 3️⃣ Least Privilege & Tiered Administration Model

Principle: Limit permissions to reduce lateral movement impact.

### Best Practices
- Minimize Domain Admin usage
- No shared admin accounts
- Separate privileged admin accounts
- Remove unnecessary group memberships
- Regular access reviews

### Tiered Administration Model
- Tier 0 → Domain Controllers, Enterprise Admins
- Tier 1 → Member Servers
- Tier 2 → Workstations

Strict separation prevents credential exposure from lower-tier systems affecting Tier 0 assets.

### SOC Monitoring Focus
Alert on:
- Non-Tier 0 systems authenticating to Domain Controllers
- Domain Admin logins to workstations
- Privilege escalation attempts
- Sudden group membership changes (Event ID 4728, 4729, 4732)

---

# 🛑 4️⃣ Protection Against Common AD Attacks

## Common Attack Techniques

- Pass-the-Hash (PtH)
- Pass-the-Ticket (PtT)
- Kerberoasting
- Golden Ticket
- Silver Ticket
- DCSync
- LLMNR/NBT-NS Poisoning
- Credential Dumping (Mimikatz)

---

## Defensive Controls & Detection

### Pass-the-Hash Mitigation
- Enable Credential Guard
- Disable NTLM
- Restrict local admin reuse (LAPS)

### Kerberoasting Mitigation
- Use strong service account passwords
- Prefer AES encryption
- Monitor abnormal TGS requests (Event ID 4769)

### Golden/Silver Ticket Mitigation
- Monitor abnormal TGT lifetimes
- Reset KRBTGT account (twice during compromise)
- Monitor unusual domain controller replication

### DCSync Detection
Alert on:
- Event ID 4662 (Directory replication)
- Non-DC accounts requesting replication privileges

### LLMNR/NBT-NS Mitigation
- Disable LLMNR via GPO
- Disable NetBIOS over TCP/IP

---

# 📊 SOC Detection Strategy

### Build Detection Use Cases For:
- Lateral movement attempts
- Privilege escalation
- Abnormal Kerberos activity
- Suspicious PowerShell usage
- Unusual service creation
- Mass authentication failures
- Logins from unusual geolocations

### Centralized Monitoring
- SIEM integration
- Log correlation
- Behavioral baselining
- Threat hunting for AD anomalies

---

# 🔄 5️⃣ Recovery & Post-Compromise Plan

Active Directory compromise = critical severity incident.

### Preparation
- Regular system state backups of Domain Controllers
- Offline & immutable backups
- Documented incident response playbook
- Test AD recovery procedures

### During Compromise
- Isolate affected systems
- Reset all privileged credentials
- Reset KRBTGT account (twice)
- Rebuild compromised Domain Controllers if needed
- Audit all trust relationships

### Post-Incident
- Conduct forensic analysis
- Identify initial access vector
- Patch vulnerabilities
- Improve logging & detection rules
- Revalidate least privilege implementation

---

# ✅ Blue Team Hardening Checklist

- Enforce MFA for privileged users  
- Disable legacy authentication protocols  
- Implement Tiered Admin Model  
- Enable detailed AD auditing  
- Forward logs to SIEM  
- Monitor Kerberos & replication activity  
- Regularly review privileged groups  
- Maintain tested AD recovery plan  

---

# 🧠 Key Blue-Team Takeaways

- AD is the backbone of enterprise identity — protect it as Tier 0.
- Most enterprise breaches escalate through AD privilege abuse.
- Prevention alone is insufficient — monitoring & detection are critical.
- Least Privilege significantly limits attacker blast radius.
- Recovery readiness is as important as prevention.

---

✅ Room Completed: Active Directory Hardening  
🎯 Focus: SOC Monitoring | Detection Engineering | Enterprise AD Defense  