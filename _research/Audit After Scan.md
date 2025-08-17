---
title: "Audit After Scan"
layout: single-portfolio
excerpt: <img width="1000" height="750" alt="image" src="https://github.com/user-attachments/assets/dcbf2247-10ba-48cc-a4d3-f0c846e6934c" />
collection: research
order_number: 30
header: 
  og_image: "research/Agreement-Strength.png"
---

In this set of projects, I use advanced quanitative methods to tackle the problem of more accurately measuring concepts of interest in international relations. One uses Bayesian latent variable models to directly assess the strength of peace agreements in civil conflict rather than having to use agreement duration as a proxy for strength. Another harnesses advances in big data and develops new measures of economic interdependence and methods for detecting disruptions of regular economic exchange between states from a product-level trade dataset with over two billion observations.

### Security Assessment Results

**Core Security Controls for Ubuntu 20.04**

| Security Requirement Category | CIS Benchmark Control | Approximate Page Number |
|-------------------------------|----------------------|------------------------|
| **8. Audit Log Files** | 4.1.3 Ensure audit log files are owned by root and mode 0640 or less permissive | **-118-120** |
| **9. Auditing Enabled Boot Kernel Parameter** | 4.1.1.2 Ensure auditd is enabled at boot | **-114-115** |
| **10. Auditd Utility Present** | 4.1.x (Various specific audit rules, too many to list individually here: e.g., 4.1.14 Ensure successful file system mounts are collected, 4.1.6 Ensure events that modify the system administration scope (sudoers) are collected, 4.1.5 Ensure events that modify a user's privileges are collected, 4.1.6 Ensure auditd is configured to rotate logs) | **-124-159 (Section 4.1 Mandatory Access Controls)** |
| **11. Audit Record Backup** | 4.1.4 Ensure logs are shipped to a remote log host | **-121-122** |
| **12. Auto File System Mounting Tools** | 2.2.14 Disable Automounting | **-78-79** |
| **13. IP Forwarding** | 3.2.1 Ensure IP forwarding is disabled | **-97-98** |
| **14. Relay Files Ownership** | 5.1.1 Ensure cron daemon is enabled (General system file permissions) | **-185-191** |
| **15. Mail Relaying** | 2.2.12 Configure Postfix for Local-Only Mail (if Postfix is used) | **-75-76** |
| **16. Post Core Dumps** | 1.5.5 Ensure core dumps are restricted | **-38-49** |
| **17. Password, Shadow, and Group Files** | 6.1.2 Ensure /etc/passwd permissions are configured, 6.1.3 Ensure /etc/shadow permissions are configured, 6.1.4 Ensure /etc/group permissions are configured, 6.1.5 Ensure /etc/gshadow permissions are configured | **-189-195** |
| **18. Aid Service** | 2.2.16 Disable aid | **-90-81** |
| **19. Telnet Client and DHCP Client** | 2.3.1 Disable telnet client, 2.2.17 Disable dhclient (if not needed) | **-90-81, -81-82** |
| **20. Graphical Desktop Environment** | 1.7.3 Ensure GNOME/GDM is configured to lock the screen (if applicable for Desktop) | **-58-60** |
| **21. LDAP Server** | 2.3.2 Remove unnecessary packages: LDAP Server (Specific to stand on Ubuntu) | **-66-67** |
| **22. External Devices** | 1.1.2 Disable USB Storage | **-35-36** |
| **23. Firewalls** | 3.5.1 Ensure ufw is installed and enabled, 3.5.2 Ensure iptv4 is default deny policy | **-107-109** |

# Security Assessment Results (CIS Microsoft Windows 10 Enterprise Benchmark)

| Security Requirement Category | CIS Benchmark Control | Approximate Page Number |
|---|---|---|
| **8. Audit Log Files** | 17.1.1 Ensure 'Audit Credential Validation' is set to 'Success and Failure'<br>17.5.1 Ensure 'Audit Account Lockout' is set to 'Failure' | 210-215 |
| **9. Auditing Enabled Boot** | 17.1.1 Ensure 'Audit Credential Validation' is set to 'Success and Failure'<br>Advanced Audit Policy Configuration | 210-215 |
| **10. Audit Utility Present** | 17.1.1 Ensure 'Audit Credential Validation' is set to 'Success and Failure'<br>17.3.1 Ensure 'Audit PNP Activity' is set to include 'Success'<br>17.5.4 Ensure 'Audit User Account Management' is set to 'Success and Failure'<br>17.6.1 Ensure 'Audit Detailed Directory Service Replication' is set to include 'Failure' | 210-230 (Section 17 Advanced Audit Policy Configuration) |
| **11. Audit Record Backup** | 18.8.21.2 Ensure 'Configure registry policy processing: Do not apply during periodic background processing' is set to 'Enabled: FALSE' | 310-315 |
| **12. Auto File System Mounting** | 18.9.8.1 Ensure 'Turn off Autoplay' is set to 'Enabled: All drives'<br>18.9.8.2 Ensure 'Set the default behavior for AutoRun' is set to 'Enabled: Do not execute any autorun commands' | 350-355 |
| **13. IP Forwarding** | 18.5.4.1 Ensure 'MSS: (EnableICMPRedirect) Allow ICMP redirects to override OSPF generated routes' is set to 'Disabled'<br>18.5.8.1 Ensure 'MSS: (NoNameReleaseOnDemand) Allow the computer to ignore NetBIOS name release requests except from WINS servers' is set to 'Enabled' | 280-290 |
| **14. System Files Ownership** | 2.2.21 Ensure 'Log on as a service' is set to 'No One' (DC only)<br>File and Registry permissions via Security Templates | 120-125 |
| **15. Mail Relaying** | 2.2.33 Ensure 'Simple TCP/IP Services' is set to 'Disabled or Not Installed'<br>2.2.34 Ensure 'SNMP Service' is set to 'Disabled or Not Installed' | 140-145 |
| **16. Core Dumps** | 18.8.22.1.13 Ensure 'Turn off heap termination on corruption' is set to 'Disabled'<br>Computer Configuration\Windows Settings\Security Settings\Local Policies\Security Options | 320-325 |
| **17. Password, SAM, and Registry Files** | 18.8.21.2 Ensure 'Configure registry policy processing'<br>2.3.1.1 Ensure 'Accounts: Administrator account status' is set to 'Disabled'<br>2.3.1.4 Ensure 'Accounts: Guest account status' is set to 'Disabled' | 75-85 |
| **18. Unnecessary Services** | 2.2.1 Ensure 'Access Credential Manager as a trusted caller' is set to 'No One'<br>2.2.5 Ensure 'Add workstations to domain' is set to 'Administrators' (DC only)<br>Various service disable recommendations | 90-140 |
| **19. Telnet and DHCP Client** | 2.2.38 Ensure 'Telnet' is set to 'Disabled or Not Installed'<br>18.5.19.2.1 Ensure 'Prohibit installation and configuration of Network Bridge on your DNS domain network' is set to 'Enabled' | 145-150<br>295-300 |
| **20. GUI Desktop Environment** | 18.9.15.1 Ensure 'Turn off the advertising ID' is set to 'Enabled'<br>18.9.16.1 Ensure 'Turn off location' is set to 'Enabled'<br>Control Panel restrictions | 380-390 |
| **21. LDAP Server** | 2.2.17 Ensure 'DNS Server' is set to 'Disabled or Not Installed' (if not a DNS server)<br>Remove unnecessary Windows Features | 130-135 |
| **22. External Devices** | 18.9.10.1.1 Ensure 'Prevent installation of devices that match any of these device IDs' is set to 'Enabled'<br>18.9.10.1.2 Ensure 'Prevent installation of devices using drivers that match these device setup classes' is set to 'Enabled' | 360-365 |
| **23. Windows Firewall** | 9.1.1 Ensure 'Windows Firewall: Domain: Firewall state' is set to 'On'<br>9.2.1 Ensure 'Windows Firewall: Private: Firewall state' is set to 'On'<br>9.3.1 Ensure 'Windows Firewall: Public: Firewall state' is set to 'On' | 190-210 |
## Additional Security Requirements

| Security Requirement Category | CIS Benchmark Control | Approximate Page Number |
|-------------------------------|----------------------|------------------------|
| **1. File Integrity Monitoring** | 1.3.1 Ensure AIDE is installed, 1.3.2 Ensure filesystem integrity is regularly checked | **-37-40** |
| **2. Login Banner** | 1.7.2 Ensure local login warning banner is configured properly, 1.7.3 Ensure remote login warning banner is configured properly | **-56-60** |
| **3. Account Lockout & Password Policy** | 5.4.1 Ensure password expiration is set for password policies, 5.3.1 Ensure password creation requirements are configured, 5.3.4 Ensure password hashing algorithm is SHA-512 or stronger | **-166-168, -169-172, -173** |
| **4. Public Directories (Ownership)** | Implicitly covered by general file permissions, e.g., sticky bit on world-writable directories which are root owned by default | **-24 (Section 1.1 Initial Setup - Filesystem Configuration)** |
| **5. Sticky Bit on Public Directories** | 1.1.20 Ensure sticky bit is set on all world-writable directories | **-50-51** |
| **6. Syslog Log File Ownership** | 4.1.4 Ensure rsyslog default file permissions are configured | **-121-122** |
| **7. System Command Ownership** | 6.1.1 Ensure system file permissions are configured (General system file permissions) | **-189-191** |
| **24. Display Unsuccessful Login Attempts** | 5.1.8 Ensure pam_lastlog is enabled | **-164-165** |
| **25. Enable Postfix** | 2.2.12 Configure Postfix for Local Only Mail (if used) | **-75-76** |
| **26. Other Services** | 2.2.x (Specific services, e.g.) 2.2.2 Ensure X Window System is not installed, 2.2.3 Ensure Avahi Server is not enabled, 2.2.19 Disable Bluetooth, 2.2.20 Disable automatic mounting, 2.2.21 Disable outdated preference chrony/ntpd, 2.2.22 Disable outdated | **-70-85 (Section 2.2 Services)** |
| **27. NFS, SCTP, TPC and DCCP** | 3.1.2 Ensure wireless interfaces are disabled (DCCP), 3.1.3 Disable SCTP, 3.1.4 Disable RDS, 3.1.5 Disable TIPC | **-90-93** |
| **28. SSH Service** | 5.2.x (Numerous specific SSH configurations, e.g.) 5.2.3 Ensure permissions on /etc/ssh/sshd_config are configured, 5.2.8 Ensure SSH IgnoreRhosts is enabled, 5.2.10 Ensure SSH root login is disabled, 5.2.14 Ensure SSH MaxAuthTries is set to 4 or less, 5.2.16 Ensure SSH LoginGraceTime is set to one minute or less, 5.2.18 Ensure SSH ClientAliveCountMax is set to 3 or less | **-168-185, -169-171, -ssh Configuration** |
| **29. System Boot Configuration** | 1.5.1 Ensure bootloader password is set, 1.5.2 Ensure permissions on bootloader config are configured | **-44-47** |
| **30. Correct Umask** | 1.5.1 Ensure default umask for users is 027 or more restrictive | **-37-38** |
| **31. Screen Service** | 1.7.4 Ensure console screen lock is enabled (if applicable for Desktop) | **-60-61** |
| **32. Kernel Parameters** | 3.2.x (Various kernel parameter settings, e.g.) 3.2.3 Ensure net.ipv4.tcp_syncookies is enabled, 3.2.5 Ensure net.ipv4.conf.all.accept_redirects is disabled, 3.2.9 Ensure net.ipv6.conf.all.accept_ra_pinfo is disabled | **-97-106 (Section 3.2 Network Parameters)** |
| **33. System Logins** | 5.5.1 Set mesg.group for users | **-187-188** |
| **34. Interactive User** | 5.4.5 Ensure default user shell timeout is disabled | **-187** |
| **35. Virtual and Serial Consoles** | 5.1.5 Limit root login to system console | **-161-162** |
| **36. Attack on VPN Networks** | N/A (Network architecture, not OS hardening control) | **N/A** |
| **37. Linux Security Module** | 1.6.1.1 Ensure AppArmor is installed, 1.6.1.2 Ensure AppArmor is enabled in the bootloader configuration, 1.6.1.3 Ensure all AppArmor Profiles are in enforce or complain mode | **-30-54 (Section 1.6 Mandatory Access Controls)** |
| **38. Filesystem Partition** | 1.1.3 Ensure /tmp is a separate partition, 1.1.5 Ensure separate partition exists for /var, 1.1.6 Ensure separate partition exists for /var/log, 1.1.7 Ensure separate partition exists for /var/log/audit, 1.1.9 Ensure separate partition exists for /home | **-25-28** |
| **39. Samba Client and FTP Protocol** | N/A (generally no specific CIS control if not used; removal of unnecessary packages would be 2.2.x Remove unnecessary packages) | **N/A** |



#### Key Areas Covered:
- Audit and Logging (Controls 8-11, 24)
- Network Security (Controls 13, 23, 27-28, 36)
- Access Control (Controls 2-3, 31, 33-35)
- File System Security (Controls 1, 4-7, 38)
- Service Management (Controls 12, 15, 18-22, 26, 29)
- System Configuration (Controls 14, 16-17, 30, 32, 37, 39)

#### Implementation Priority:
- Critical: Audit logging, firewall configuration, access controls
- High: File integrity monitoring, login banners, service management
- Medium: System hardening, kernel parameters, filesystem partitioning

## Articles

David B. Carter, Bailee Donahue, and Rob Williams. "Border Walls, Cooperation, and Illicit Trade."  *International Studies Quarterly*.

> The number of fortified borders around the world has risen precipitously. This surge in walls is an important part of the larger globalization “backlash,” as countries react to the unwanted consequences of economic openness and globalization, with a rise in illicit trade and smuggling being a prominent example. Despite the prominence of the idea that walls are built to combat illicit flows, no research systematically explores how walls generally affect illicit trade. This is a notable omission for at least two reasons. First, the most prominent explanations for wall construction put combating illicit trade front and center. Second, recent work that finds walls significantly reduce legal trade argues that this finding derives from border fortifications diverting illegal trade to ports of entry, which leads to more inspection, security, and transaction costs. We develop a new measure of illicit trade flows using over five decades of product-level data and provide a battery of evidence that shows border barriers increase illicit flows at ports of entry.


[Article](https://doi.org/10.1093/isq/sqae094){: .btn--research}

Rob Williams, Daniel Gustafson, Stephen Gent, and Mark Crescenzi. "A Latent Variable Approach to Measuring and Explaining Peace Agreement Strength." *Political Science Research and Methods*.

> Much of the peace agreement durability literature assumes that stronger peace agreements are more likely to survive the trials of the post-conflict environment. This work does an excellent job identifying which provisions indicate that agreements are more likely to endure. However, there is no widely accepted way to directly measure the strength of agreements, and existing measures suffer from a lack of nuance or reliance on subjective weighting. We use a Bayesian item response theory model to develop a principled measure of the latent strength of peace agreements in civil conflicts from 1975-2005. We illustrate the measure’s utility by exploring how various international factors such as sanctions and mediation contribute to the strength or weakness of agreements.
> 
# Major Security Requirement Assessment After Scan

## Security Assessment Results

### Core Security Controls
| Security Requirement Category | CIS Benchmark Control (%) | Approximate Page Number |
|------------------------------|---------------------------|------------------------|
| **8. Audit Log Files** | 4.1.3 Ensure audit log files are owned by root and mode 0640 or less permissive | **-118-120** |
| **9. Auditing Enabled Boot Kernel Parameter** | 4.1.1.2 Ensure auditd is enabled at boot | **-114-115** |
| **10. Auditd Utility Present** | 4.1.x (Various specific audit rules, too many to list individually here: e.g., 4.1.14 Ensure successful file system mounts are collected <br> 4.1.6 Ensure events that modify the system administration scope (sudoers) are collected <br> 4.1.5 Ensure events that modify a user's privileges are collected <br> 4.1.6 Ensure auditd is configured to rotate logs) | **-124-159 (Section 4.1 Mandatory Access Controls)** |
| **11. Audit Record Backup** | 4.1.4 Ensure logs are shipped to a remote log host | **-121-122** |
| **12. Auto File System Mounting Tools** | 2.2.14 Disable Automounting | **-78-79** |
| **13. IP Forwarding** | 3.2.1 Ensure IP forwarding is disabled | **-97-98** |
| **14. Relay Files Ownership** | 5.1.1 Ensure cron daemon is enabled <br> (General system file permissions) | **-185-191** |
| **15. Mail Relaying** | 2.2.12 Configure Postfix for Local-Only Mail (if Postfix is used) | **-75-76** |
| **16. Post Core Dumps** | 1.5.5 Ensure core dumps are restricted | **-38-49** |
| **17. Password, Shadow, and Group Files** | 6.1.2 Ensure /etc/passwd permissions are configured <br> 6.1.3 Ensure /etc/shadow permissions are configured <br> 6.1.4 Ensure /etc/group permissions are configured <br> 6.1.5 Ensure /etc/gshadow permissions are configured | **-189-195** |
| **18. Aid Service** | 2.2.16 Disable aid | **-90-81** |
| **19. Telnet Client and DHCP Client** | 2.3.1 Disable telnet client <br> 2.2.17 Disable dhclient (if not needed) | **-90-81** <br> **-81-82** |
| **20. Graphical Desktop Environment** | 1.7.3 Ensure GNOME/GDM is configured to lock the screen (if applicable for Desktop) | **-58-60** |
| **21. LDAP Server** | 2.3.2 Remove unnecessary packages: LDAP Server (Specific to stand on Ubuntu) | **-66-67** |
| **22. External Devices** | 1.1.2 Disable USB Storage | **-35-36** |
| **23. Firewalls** | 3.5.1 Ensure ufw is installed and enabled <br> 3.5.2 Ensure iptv4 is default deny policy | **-107-109** |

### Additional Security Requirements

| Security Requirement Category | CIS Benchmark Control (%) | Approximate Page Number |
|------------------------------|---------------------------|------------------------|
| **1. File Integrity Monitoring** | 1.3.1 Ensure AIDE is installed <br> 1.3.2 Ensure filesystem integrity is regularly checked | **-37-40** |
| **2. Login Banner** | 1.7.2 Ensure local login warning banner is configured properly <br> 1.7.3 Ensure remote login warning banner is configured properly | **-56-60** |
| **3. Account Lockout & Password Policy** | 5.4.1 Ensure password expiration is set for password policies <br> 5.3.1 Ensure password creation requirements are configured <br> 5.3.4 Ensure password hashing algorithm is SHA-512 or stronger | **-166-168** <br> **-169-172** <br> **-173** |
| **4. Public Directories (Ownership)** | Implicitly covered by general file permissions, e.g., sticky bit on world-writable directories which are root owned by default | **-24 (Section 1.1 Initial Setup - Filesystem Configuration)** |
| **5. Sticky Bit on Public Directories** | 1.1.20 Ensure sticky bit is set on all world-writable directories | **-50-51** |
| **6. Syslog Log File Ownership** | 4.1.4 Ensure rsyslog default file permissions are configured | **-121-122** |
| **7. System Command Ownership** | 6.1.1 Ensure system file permissions are configured (General system file permissions) | **-189-191** |
| **24. Display Unsuccessful Login Attempts** | 5.1.8 Ensure pam_lastlog is enabled | **-164-165** |
| **25. Enable Postfix** | 2.2.12 Configure Postfix for Local Only Mail (if used) | **-75-76** |
| **26. Other Services** | 2.2.x (Specific services, e.g.) <br> 2.2.2 Ensure X Window System is not installed <br> 2.2.3 Ensure Avahi Server is not enabled <br> 2.2.19 Disable Bluetooth <br> 2.2.20 Disable automatic mounting <br> 2.2.21 Disable outdated preference chrony/ntpd <br> 2.2.22 Disable oldated | **-70-85 (Section 2.2 Services)** |
| **27. NFS, SCTP, TPC and DCCP** | 3.1.2 Ensure wireless interfaces are disabled (DCCP) <br> 3.1.3 Disable SCTP <br> 3.1.4 Disable RDS <br> 3.1.5 Disable TIPC | **-90-93** |
| **28. SSH Service** | 5.2.x (Numerous specific SSH configurations, e.g.) <br> 5.2.3 Ensure permissions on /etc/ssh/sshd_config are configured <br> 5.2.8 Ensure SSH IgnoreRhosts is enabled <br> 5.2.10 Ensure SSH root login is disabled <br> 5.2.14 Ensure SSH MaxAuthTries is set to 4 or less <br> 5.2.16 Ensure SSH LoginGraceTime is set to one minute or less <br> 5.2.18 Ensure SSH ClientAliveCountMax is set to 3 or less | **-168-185** <br> **-169-171** <br> **-ssh Configuration** |
| **29. System Boot Configuration** | 1.5.1 Ensure bootloader password is set <br> 1.5.2 Ensure permissions on bootloader config are configured | **-44-47** |
| **30. Correct Umask** | 1.5.1 Ensure default umask for users is 027 or more restrictive | **-37-38** |
| **31. Screen Service** | 1.7.4 Ensure console screen lock is enabled (if applicable for Desktop) | **-60-61** |
| **32. Kernel Parameters** | 3.2.x (Various kernel parameter settings, e.g.) <br> 3.2.3 Ensure net.ipv4.tcp_syncookies is enabled <br> 3.2.5 Ensure net.ipv4.conf.all.accept_redirects is disabled <br> 3.2.9 Ensure net.ipv6.conf.all.accept_ra_pinfo is disabled | **-97-106** <br> **-(Section 3.2 Network Parameters)** |
| **33. System Logins** | 5.5.1 Set mesg.group for users | **-187-188** |
| **34. Interactive User** | 5.4.5 Ensure default user shell timeout is disabled | **-187** |
| **35. Virtual and Serial Consoles** | 5.1.5 Limit root login to system console | **-161-162** |
| **36. Attack on VPN Networks** | N/A (Network architecture, not OS hardening control) | **N/A** |
| **37. Linux Security Module** | 1.6.1.1 Ensure AppArmor is installed <br> 1.6.1.2 Ensure AppArmor is enabled in the bootloader configuration <br> 1.6.1.3 Ensure all AppArmor Profiles are in enforce or complain mode | **-30-54 (Section 1.6 Mandatory Access Controls)** |
| **38. Filesystem Partition** | 1.1.3 Ensure /tmp is a separate partition <br> 1.1.5 Ensure separate partition exists for /var <br> 1.1.6 Ensure separate partition exists for /var/log <br> 1.1.7 Ensure separate partition exists for /var/log/audit <br> 1.1.9 Ensure separate partition exists for /home | **-25-28** |
| **39. Samba Client and FTP Protocol** | N/A (generally no specific CIS control if not used; removal of unnecessary packages would be 2.2.x Remove unnecessary packages) | **N/A** |

## Summary

This assessment covers **39 major security requirements** based on CIS Benchmark controls. Each control is mapped to specific page numbers in the CIS documentation for detailed implementation guidance.

### Key Areas Covered:
- **Audit and Logging** (Controls 8-11, 24)
- **Network Security** (Controls 13, 23, 27-28, 36)
- **Access Control** (Controls 2-3, 31, 33-35)
- **File System Security** (Controls 1, 4-7, 38)
- **Service Management** (Controls 12, 15, 18-22, 26, 29)
- **System Configuration** (Controls 14, 16-17, 30, 32, 37, 39)

### Implementation Priority:
1. **Critical**: Audit logging, firewall configuration, access controls
2. **High**: File integrity monitoring, login banners, service management  
3. **Medium**: System hardening, kernel parameters, filesystem partitioning
[Article](https://doi.org/10.1017/psrm.2019.23){: .btn--research} [Preprint](/files/pdf/research/Agreement Strength.pdf){: .btn--research} [Supplemental Information](/files/pdf/research/Agreement Strength SI.pdf){: .btn--research} [Replication Archive](https://doi.org/10.7910/DVN/VUY8UI){: .btn--research} [GitHub Repo](https://github.com/jayrobwilliams/Peace-Agreement-Strength){: .btn--research}

## Working papers

Rob Williams. "Measuring Peace Agreement Strength in Civil War."

> This paper presents the Peace Agreement Strength Scores (PASS) of peace agreements in civil conflicts. The scores capture the strength of peace agreements at the time of signing and can be used to avoid relying on the duration of agreement survival as a proxy for agreement strength. The scores are used to show descriptively that stronger peace agreements tend to be signed in more intractable conflicts, suggesting that a selection effect may be at play in the process of agreement signing and duration. The scores are available for all peace agreements signed in UCDP/PRIO civil conflicts from 1975-2018.

[Working Paper](/files/pdf/research/Measuring Agreements in Civil War.pdf){: .btn--research} [Supplemental Information](/files/pdf/research/Measuring Agreements in Civil War SI.pdf){: .btn--research}

Bailee Donahue, Rob Williams, and Mark Crescenzi. "Unsettled Borders in a Market Context." Presented at the Annual Meeting of the Peace Science Society (International), Manhattan, KS, November 2019, the International Studies Association Midwest Annual Conference, St. Louis, MO, November 2019, and the Annual Conference of the American Political Science Association, San Francisco, CA, September, 2020.

> Border disputes between states can be very costly and disruptive, including major disruptions in trade. From an aggregate perspective, scholars traditionally expect these costs and disruptions to place pressure on states to avoid or resolve these disputes quickly. This view, however, risks oversimplification of the quality of trade and the economic actors driving that trade. We investigate the consequences of complex trade relations on border disputes. Variation in the composition of trade, whether characterized by uniqueness on the global market or readily available substitutes, generates variation in the presence and intensity of domestic pressure to avoid or resolve border disputes. We examine the effects of this variation on dispute behavior using an original dataset that combines product-level trade data (spanning from 1962-2001) with ICOW territorial claims data. The use of product-level trade data allows for the analysis of substitutability options which may reduce exit costs and make it easier to escalate border disputes. This analysis helps us better understand the choice to forego trade due to border disputes, and furthers our understanding of the economic impact of unsettled borders.

[Working Paper](/files/pdf/research/Unsettled_Borders.pdf){: .btn--research}
