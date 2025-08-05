---
title: "Remediation"
layout: single-portfolio
excerpt: <img width="1400" height="800" alt="image" src="https://github.com/user-attachments/assets/3706eba1-a06a-4673-93ad-8091d5632eb5" />
collection: research
order_number: 40
header: 
  og_image: "research/ternary.png"
---

In this thesis the researcher has given a proper "REMEDIATION" to vulnerabilities found during the scans in the form of code with respect to individual vulnereabilities.

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
