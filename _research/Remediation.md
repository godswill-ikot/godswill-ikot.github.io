---
title: "Remediation"
layout: single-portfolio
excerpt: <img width="1400" height="800" alt="image" src="https://github.com/user-attachments/assets/3706eba1-a06a-4673-93ad-8091d5632eb5" />
collection: research
order_number: 40
header: 
  og_image: "research/ternary.png"
---

In this thesis the researcher has given a proper "REMEDIATION" steps to vulnerabilities found during the scans in the form of code with respect to individual vulnereabilities.
The CIS-CAT on Ubuntu 20.04 and Windows_10_Ent encourage 'MANUAL' remediation while OpenSCAP give a combined method 'Automated and Manual'.
Remediation is divided into 2 parts, with the first 1st being Full Remediation and the second 2nd is Selective Remediation.
#### Option A: Full Generated Script using OpenSCAP (CAUTION) for Ubuntu 20.04
```bash
# BACKUP FIRST - This will make system-wide changes
# Create restoration point
sudo cp /etc/passwd /etc/passwd.pre-remediation
sudo cp /etc/shadow /etc/shadow.pre-remediation
sudo cp -r /etc/ssh /etc/ssh.pre-remediation

# Generate remediation script for CIS Level 1 Workstation
oscap xccdf generate fix \
    --profile xccdf_org.ssgproject.content_profile_cis_level1_workstation \
    --output ~/openscap-results/baseline/cis-l1-workstation-remediation.sh \
    /usr/share/xml/scap/ssg/content/ssg-ubuntu2004-ds.xml
# Generate remediation script for CIS Level 2 Workstation
oscap xccdf generate fix \
    --profile xccdf_org.ssgproject.content_profile_cis_level2_workstation \
    --output ~/openscap-results/baseline/cis-l2-workstation-remediation.sh \
    /usr/share/xml/scap/ssg/content/ssg-ubuntu2004-ds.xml

# Make remediation scripts executable
chmod +x ~/openscap-results/baseline/cis-l*-workstation-remediation.sh

# Run the full remediation
sudo ./cis-l1-workstation-remediation.sh 2>&1 | tee remediation-log.txt
```
#### Option B: Selective Remediation using recommendations from CIS-CAT (**RECOMMENDED**) for for Ubuntu 20.04
```bash
# Extract specific remediation commands and run them individually

# Example: Fix file permissions
echo "=== Fixing file permissions ==="
sudo chmod 644 /etc/passwd
sudo chmod 600 /etc/shadow
sudo chmod 600 /etc/gshadow
sudo chmod 644 /etc/group

# Example: Configure system auditing
echo "=== Installing and configuring audit daemon ==="
sudo apt install -y auditd audispd-plugins
sudo systemctl enable auditd
sudo systemctl start auditd

# Example: Configure login banner
echo "=== Setting up login banner ==="
sudo tee /etc/issue << 'EOF'
WARNING: Unauthorized access to this system is prohibited.
All connections are monitored and recorded.
EOF

sudo tee /etc/issue.net << 'EOF'
WARNING: Unauthorized access to this system is prohibited.
All connections are monitored and recorded.
EOF
```
Verify Remediation Results using Lynis, OpenSCAP and CIS-CAT for Ubuntu 20.04
```bash
Use LYNIS for deep scan
sudo lynis audit system # Test run system audit
                  OR
# Re-run the assessment to check improvements
mkdir -p ~/openscap-results/post-remediation
# Run post-remediation assessment
oscap xccdf eval \
    --profile xccdf_org.ssgproject.content_profile_cis_level1_workstation \
    --results ~/openscap-results/post-remediation/cis-l1-post-remediation-results.xml \
    --report ~/openscap-results/post-remediation/cis-l1-post-remediation-report.html \
    /usr/share/xml/scap/ssg/content/ssg-ubuntu2004-ds.xml

# Compare before and after
```
Rollback Procedure (If Needed) for Ubuntu 20.04
```bash
# Create rollback script
cat > rollback-remediation.sh << 'EOF'
#!/bin/bash
echo "Rolling back remediation changes..."
# Restore from backup
BACKUP_DIR="/root/openscap-backup/$(ls -1 /root/openscap-backup/ | tail -1)"
if [ -d "$BACKUP_DIR" ]; then
    cp -r $BACKUP_DIR/ssh /etc/
    cp $BACKUP_DIR/login.defs /etc/
    systemctl restart ssh
    echo "Rollback completed from: $BACKUP_DIR"
else
    echo "No backup directory found!"
fi
EOF

chmod +x rollback-remediation.sh
```
Monitoring and Maintenance for Ubuntu 20.04
```bash
# Set up regular compliance checking
cat > /etc/cron.weekly/openscap-check << 'EOF'
#!/bin/bash
/usr/local/bin/oscap xccdf eval \
    --profile xccdf_org.ssgproject.content_profile_cis_level1_workstation \
    --results /var/log/openscap/weekly-$(date +%Y%m%d)-results.xml \
    --report /var/log/openscap/weekly-$(date +%Y%m%d)-report.html \
    /usr/share/xml/scap/ssg/content/ssg-ubuntu2004-ds.xml
EOF

sudo mkdir -p /var/log/openscap
sudo chmod +x /etc/cron.weekly/openscap-check
```
#### Manual Remediation for Windows_10 using
```powershell
# Windows Security Remediation - PowerShell 7 Manual Commands
# CIS Microsoft Windows 10 Enterprise Benchmark v4.0.0 Level 1
# Prerequisites: 
# - PowerShell 7.0+
# - Administrator privileges: Requires -RunAsAdministrator 
# - Windows 10
# =================================
# GROUP 1: INITIAL SETUP - Easy Implementation Controls
# =================================
# Windows Update Automatic Policies (Critical Impact)
Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU" -Name "NoAutoUpdate" -Value 0 -Type DWord -Force
Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU" -Name "AUOptions" -Value 4 -Type DWord -Force
Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU" -Name "ScheduledInstallDay" -Value 0 -Type DWord -Force
Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU" -Name "ScheduledInstallTime" -Value 3 -Type DWord -Force
# Storage Sense Automated Cleanup (Medium Impact)
Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\StorageSense" -Name "AllowStorageSenseGlobal" -Value 1 -Type DWord -Force
Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\StorageSense" -Name "AllowStorageSenseTemporaryFilesCleanup" -Value 1 -Type DWord -Force
Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\StorageSense" -Name "StorageSenseCloudContentDehydrationThreshold" -Value 30 -Type DWord -Force
# System Restore Point Policies (Medium Impact)
Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\SystemRestore" -Name "DisableConfig" -Value 0 -Type DWord -Force
Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\SystemRestore" -Name "DisableSR" -Value 0 -Type DWord -Force
Enable-ComputerRestore -Drive "C:\"
Checkpoint-Computer -Description "Security Remediation Baseline" -RestorePointType "MODIFY_SETTINGS"
# Disk Quota Management (Medium Impact) - Enable quota management for system drives
fsutil quota enforce C:
fsutil quota modify C: 10737418240 8589934592 Administrator
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Control\FileSystem" -Name "NtfsDisableLastAccessUpdate" -Value 1 -Type DWord -Force
# ===============
# GROUP 2: SERVICES - Easy Implementation Controls  
# ===============
# Task Scheduler Security Policies (Medium Impact)
Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Schedule" -Name "DisableRpcOverTcp" -Value 1 -Type DWord -Force
Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\Task Scheduler5.0" -Name "Disable New Task Creation" -Value 0 -Type DWord -Force
Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\Task Scheduler5.0" -Name "Allow Cross Forest Tasks" -Value 0 -Type DWord -Force
# Disable Unnecessary Services (Medium Impact)
$servicesToDisable = @(
    "TabletInputService",        # Tablet PC Input Service
    "WSearch",                   # Windows Search (if not needed)
    "Spooler",                   # Print Spooler (if no printers)
    "Fax",                       # Fax Service
    "TapiSrv",                   # Telephony
    "SensorService",             # Sensor Service
    "SensrSvc",                  # Sensor Monitoring Service
    "RetailDemo",                # Retail Demo Service
    "dmwappushservice",          # Device Management Wireless Application Protocol
    "MapsBroker"                 # Downloaded Maps Manager
)

foreach ($service in $servicesToDisable) {
    if (Get-Service -Name $service -ErrorAction SilentlyContinue) {
        Stop-Service -Name $service -Force -ErrorAction SilentlyContinue
        Set-Service -Name $service -StartupType Disabled
        Write-Host "Disabled service: $service" -ForegroundColor Yellow
    }
}

# Service Failure Recovery Actions (Medium Impact)
sc.exe failure "Themes" reset= 86400 actions= restart/60000/restart/60000/restart/60000
sc.exe failure "AudioSrv" reset= 86400 actions= restart/60000/restart/60000/restart/60000
sc.exe failure "EventLog" reset= 86400 actions= restart/60000/restart/60000/restart/60000
# Service Account Restrictions (High Impact)
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Control\Lsa" -Name "RestrictAnonymous" -Value 1 -Type DWord -Force
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Control\Lsa" -Name "RestrictAnonymousSAM" -Value 1 -Type DWord -Force
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\lanmanserver\parameters" -Name "RestrictNullSessAccess" -Value 1 -Type DWord -Force
# ================
# GROUP 3: NETWORK - Easy Implementation Controls
# ================
# IPv6 Transition Security (High Impact)
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\Tcpip6\Parameters" -Name "DisabledComponents" -Value 0xFF -Type DWord -Force
Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\TCPIP\v6Transition" -Name "Force_Tunneling" -Value 0 -Type DWord -Force
Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\TCPIP\v6Transition" -Name "6to4_State" -Value 1 -Type DWord -Force
# SSL Configuration Hardening (High Impact)
# Disable SSL 2.0
New-Item -Path "HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0" -Force
New-Item -Path "HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client" -Force
New-Item -Path "HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server" -Force
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client" -Name "Enabled" -Value 0 -Type DWord -Force
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server" -Name "Enabled" -Value 0 -Type DWord -Force
# Disable SSL 3.0
New-Item -Path "HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0" -Force
New-Item -Path "HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Client" -Force
New-Item -Path "HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server" -Force
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Client" -Name "Enabled" -Value 0 -Type DWord -Force
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server" -Name "Enabled" -Value 0 -Type DWord -Force
# Network Provider Security Settings (Medium Impact)
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Control\NetworkProvider\Order" -Name "ProviderOrder" -Value "RDPNP,LanmanWorkstation,webclient" -Type String -Force
Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\Network Connections" -Name "NC_ShowSharedAccessUI" -Value 0 -Type DWord -Force
# WLAN Media Cost Policies (Medium Impact)
Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\WcmSvc\GroupPolicy" -Name "fMinimizeConnections" -Value 1 -Type DWord -Force
Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\WcmSvc\GroupPolicy" -Name "fBlockNonDomain" -Value 1 -Type DWord -Force
# Network Connection Security (High Impact)
Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\Network Connections" -Name "NC_StdDomainUserSetLocation" -Value 1 -Type DWord -Force
Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\Network Connections" -Name "NC_AllowNetBridge_NLA" -Value 0 -Type DWord -Force
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\Netbt\Parameters" -Name "NoNameReleaseOnDemand" -Value 1 -Type DWord -Force
# ==================
# GROUP 4: HOST-BASED FIREWALL - Easy Implementation Controls
# ==================
# Advanced Firewall Logging (Medium Impact)
netsh advfirewall set allprofiles logging filename %systemroot%\system32\LogFiles\Firewall\pfirewall.log
netsh advfirewall set allprofiles logging maxfilesize 4096
netsh advfirewall set allprofiles logging droppedconnections enable
netsh advfirewall set allprofiles logging allowedconnections enable
# Custom Firewall Rules (Medium Impact) - Block common attack vectors
netsh advfirewall firewall add rule name="Block WinRM HTTP" dir=in action=block protocol=TCP localport=5985
netsh advfirewall firewall add rule name="Block WinRM HTTPS" dir=in action=block protocol=TCP localport=5986
netsh advfirewall firewall add rule name="Block SMB" dir=in action=block protocol=TCP localport=445
netsh advfirewall firewall add rule name="Block NetBIOS" dir=in action=block protocol=TCP localport=139
netsh advfirewall firewall add rule name="Block RPC Endpoint Mapper" dir=in action=block protocol=TCP localport=135
# Firewall Notification Settings (Medium Impact)
Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\WindowsFirewall\DomainProfile" -Name "DisableNotifications" -Value 0 -Type DWord -Force
Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\WindowsFirewall\PrivateProfile" -Name "DisableNotifications" -Value 0 -Type DWord -Force
Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\WindowsFirewall\PublicProfile" -Name "DisableNotifications" -Value 0 -Type DWord -Force
# =======================
# GROUP 5: ACCESS CONTROL - Easy Implementation Controls
# =======================
# Enhanced UAC Settings (High Impact)
Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System" -Name "ConsentPromptBehaviorAdmin" -Value 2 -Type DWord -Force
Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System" -Name "ConsentPromptBehaviorUser" -Value 3 -Type DWord -Force
Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System" -Name "EnableInstallerDetection" -Value 1 -Type DWord -Force
Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System" -Name "ValidateAdminCodeSignatures" -Value 1 -Type DWord -Force
Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System" -Name "EnableSecureUIAPaths" -Value 1 -Type DWord -Force
Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System" -Name "EnableLUA" -Value 1 -Type DWord -Force
Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System" -Name "PromptOnSecureDesktop" -Value 1 -Type DWord -Force
# Interactive Logon Security (High Impact)
Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System" -Name "DontDisplayLastUserName" -Value 1 -Type DWord -Force
Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System" -Name "DontDisplayLockedUserId" -Value 3 -Type DWord -Force
Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System" -Name "InactivityTimeoutSecs" -Value 900 -Type DWord -Force
Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon" -Name "ScreenSaverGracePeriod" -Value 5 -Type DWord -Force
# Network Logon Restrictions (High Impact)
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Control\Lsa" -Name "LimitBlankPasswordUse" -Value 1 -Type DWord -Force
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Control\Lsa" -Name "NoLMHash" -Value 1 -Type DWord -Force
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Control\Lsa" -Name "LmCompatibilityLevel" -Value 5 -Type DWord -Force
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Control\Lsa" -Name "NTLMMinClientSec" -Value 537395200 -Type DWord -Force
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Control\Lsa" -Name "NTLMMinServerSec" -Value 537395200 -Type DWord -Force
# Session Timeout Policies (Medium Impact)
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters" -Name "autodisconnect" -Value 15 -Type DWord -Force
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters" -Name "EnableSecuritySignature" -Value 1 -Type DWord -Force
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters" -Name "RequireSecuritySignature" -Value 1 -Type DWord -Force
# ======================
# GROUP 6: LOGGING AND AUDITING - Easy Implementation Controls
# ======================
# Event Log Size Configuration (Medium Impact)
wevtutil sl Security /ms:196608000
wevtutil sl Application /ms:32768000  
wevtutil sl System /ms:32768000
wevtutil sl "Windows PowerShell" /ms:32768000
# Log Retention Policies (Medium Impact)
wevtutil sl Security /rt:false
wevtutil sl Application /rt:false
wevtutil sl System /rt:false
Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\EventLog\Security" -Name "Retention" -Value "0" -Type String -Force
Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\EventLog\Application" -Name "Retention" -Value "0" -Type String -Force
Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\EventLog\System" -Name "Retention" -Value "0" -Type String -Force
# Additional Audit Categories (Medium Impact)
auditpol /set /subcategory:"Credential Validation" /success:enable /failure:enable
auditpol /set /subcategory:"Application Group Management" /success:enable /failure:enable
auditpol /set /subcategory:"Computer Account Management" /success:enable /failure:enable
auditpol /set /subcategory:"Distribution Group Management" /success:enable /failure:enable
auditpol /set /subcategory:"Other Account Management Events" /success:enable /failure:enable
auditpol /set /subcategory:"Security Group Management" /success:enable /failure:enable
auditpol /set /subcategory:"User Account Management" /success:enable /failure:enable
auditpol /set /subcategory:"Process Creation" /success:enable /failure:enable
auditpol /set /subcategory:"Directory Service Changes" /success:enable /failure:enable
auditpol /set /subcategory:"Directory Service Replication" /success:enable /failure:enable
auditpol /set /subcategory:"Detailed Directory Service Replication" /success:enable /failure:enable
# Event Log Security Permissions (Medium Impact)
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\EventLog\Security" -Name "RestrictGuestAccess" -Value 1 -Type DWord -Force
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\EventLog\Application" -Name "RestrictGuestAccess" -Value 1 -Type DWord -Force
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\EventLog\System" -Name "RestrictGuestAccess" -Value 1 -Type DWord -Force
# ===========================
# GROUP 7: SYSTEM MAINTENANCE - Easy Implementation Controls
# ===========================
# System Settings Hardening (High Impact)
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager" -Name "SafeDllSearchMode" -Value 1 -Type DWord -Force
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager" -Name "ProtectionMode" -Value 1 -Type DWord -Force
Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System" -Name "DisableCAD" -Value 0 -Type DWord -Force
Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Setup\RecoveryConsole" -Name "SecurityLevel" -Value 0 -Type DWord -Force
Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Setup\RecoveryConsole" -Name "SetCommand" -Value 0 -Type DWord -Force
# File and Folder Permission Templates (Medium Impact)
icacls "C:\Windows\System32\config" /inheritance:r /grant:r "Administrators:(OI)(CI)F" "SYSTEM:(OI)(CI)F"
icacls "C:\Windows\System32\drivers" /inheritance:r /grant:r "Administrators:(OI)(CI)F" "SYSTEM:(OI)(CI)F" "TrustedInstaller:(OI)(CI)F"
icacls "C:\Windows\System32\spool" /inheritance:r /grant:r "Administrators:(OI)(CI)F" "SYSTEM:(OI)(CI)F"
# Registry Access Restrictions (Medium Impact)
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Control\SecurePipeServers\winreg" -Name "Description" -Value "Registry Server" -Type String -Force
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Control\SecurePipeServers\winreg" -Name "AllowedExactPaths" -Value @("System\CurrentControlSet\Control\ProductOptions", "System\CurrentControlSet\Control\Server Applications", "Software\Microsoft\Windows NT\CurrentVersion") -Type MultiString -Force
# System Maintenance Scheduling (Medium Impact)
schtasks /create /tn "Security Baseline Check" /tr "powershell.exe -ExecutionPolicy Bypass -File C:\Scripts\SecurityCheck.ps1" /sc weekly /d SUN /st 02:00 /ru SYSTEM /f
schtasks /create /tn "Event Log Cleanup" /tr "wevtutil cl Application" /sc monthly /d 1 /st 03:00 /ru SYSTEM /f
# Temporary File Cleanup Policies (Medium Impact)
Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\Storage Sense" -Name "AllowStorageSenseTemporaryFilesCleanup" -Value 1 -Type DWord -Force
Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\Storage Sense" -Name "ConfigStorageSenseRecycleBinCleanupThreshold" -Value 30 -Type DWord -Force
Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\Storage Sense" -Name "ConfigStorageSenseDownloadsCleanupThreshold" -Value 30 -Type DWord -Force
# =========================
# VERIFICATION AND RESTART RECOMMENDATIONS
# =========================
Write-Host "=== Security Remediation Complete ===" -ForegroundColor Green
Write-Host "Manual verification recommended for:" -ForegroundColor Yellow
Write-Host "1. Windows Update settings in Settings > Update & Security" -ForegroundColor White
Write-Host "2. Firewall rules in Windows Defender Firewall with Advanced Security" -ForegroundColor White  
Write-Host "3. UAC settings in Control Panel > User Accounts" -ForegroundColor White
Write-Host "4. Event log sizes in Event Viewer properties" -ForegroundColor White
Write-Host "5. Service status in services.msc" -ForegroundColor White
Write-Host ""
Write-Host "RESTART REQUIRED for some changes to take effect" -ForegroundColor Red
Write-Host "Run 'Restart-Computer -Force' when ready" -ForegroundColor Yellow
```
