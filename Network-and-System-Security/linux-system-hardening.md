# 🔐 Linux System Hardening

## 📌 Introduction

Linux systems provide a reliable and cost-effective alternative to closed-source platforms such as Windows Server and proprietary UNIX systems. Distributions like Debian 11 can be deployed without expensive licensing costs, making Linux an attractive choice for servers and enterprise environments.

However, Linux is not secure by default. Before deploying a system in production, it must be hardened to reduce the attack surface and protect against unauthorized access, exploitation, and data breaches.

**Linux Hardening** is the process of securing a Linux system through proper configuration, access control, monitoring, and continuous updates.

---

## 🎯 Learning Objectives

This topic covers how to improve Linux security through:

- Physical Security  
- Filesystem Encryption  
- Firewall Configuration  
- Secure Remote Access  
- Software & Services Management  
- Updates & Upgrades  
- Log Monitoring  

---

## 🛡️ 1. Physical Security

If an attacker gains physical access, they can compromise the entire system.

### Best Practices:
- Set BIOS/UEFI password  
- Disable booting from external media  
- Enable Secure Boot  
- Configure GRUB password  
- Restrict physical access to servers  
- Use Full Disk Encryption  

---

## 🔒 2. Filesystem Encryption

Encryption protects data at rest.

### Methods:
- **Full Disk Encryption (FDE):** LUKS, dm-crypt  
- **File-Level Encryption:** GPG, fscrypt  

### Best Practices:
- Encrypt sensitive partitions (`/home`, `/var`)  
- Use strong passphrases  
- Securely back up encryption keys  

---

## 🔥 3. Firewall Configuration

A firewall filters traffic based on defined rules.

### Common Tools:
- iptables  
- nftables  
- ufw  
- firewalld  

### Hardening Steps:
- Set default deny policy  
- Allow only required ports (e.g., 22, 80, 443)  
- Disable unused services  
- Enable logging for blocked traffic  

---

## 🌐 4. Secure Remote Access (SSH Hardening)

Remote access is a major attack vector.

### Best Practices:
- Disable root login (`PermitRootLogin no`)  
- Use SSH key-based authentication  
- Disable password authentication  
- Use Fail2Ban to prevent brute-force attacks  
- Restrict allowed users  
- Implement Multi-Factor Authentication (MFA)  

---

## 📦 5. Software & Services Management

Minimize the attack surface by reducing unnecessary software.

### Best Practices:
- Remove unused packages  
- Disable unnecessary services  
- Regularly audit open ports  
- Apply the Principle of Least Privilege  
- Use minimal installation environments  

---

## 🔄 6. Updates & Upgrades

Outdated systems are vulnerable systems.

### Best Practices:
- Regularly run system updates  
- Enable automatic security updates  
- Monitor security advisories and CVEs  
- Remove obsolete packages and kernels  

---

## 📊 7. Logs & Monitoring

Logging is essential for detecting and investigating incidents.

### Important Logs:
- `/var/log/auth.log` – Authentication logs  
- `/var/log/syslog` – System events  
- `/var/log/kern.log` – Kernel logs  

### Best Practices:
- Monitor failed login attempts  
- Enable log rotation  
- Use tools like auditd and Fail2Ban  
- Forward logs to centralized monitoring systems (SIEM)  

---

## ✅ Conclusion

Linux is secure, flexible, and cost-effective — but only when properly hardened. Linux hardening is an ongoing process that includes securing physical access, encrypting data, restricting network exposure, managing services, applying updates, and continuously monitoring logs.

Proper hardening significantly reduces attack surfaces and strengthens overall system security posture.