# Day 6 – Linux Internals for Security

## Goal
Understand Linux internals from a defender’s perspective by learning how access is controlled, how processes are monitored, and how system activity is logged and investigated. These skills are essential for SOC analysts when detecting misuse, investigating incidents, and validating system behavior.

---

## Lab Environment
- Ubuntu Server (analysis target)
- Kali Linux (external login simulation)
- Windows 10 (external login simulation)

---

## Task 1 – User & Permission Management

### Objective
Understand how Linux enforces access control using users, ownership, and file permissions, and how defenders apply the principle of least privilege.

### Actions Performed
- Created a non-privileged user to simulate a standard system user
- Switched user context to confirm authentication behavior
- Created a sensitive file owned by the root user
- Restricted file permissions so only the owner could access the file
- Changed file ownership to enforce strict access control
- Verified that unauthorized users were denied access

### Commands Used
- chmod
- chown

### Evidence
Non-privileged user created   
screenshots/day6_p1_user_created.png

Restricted permissions
screenshots/day6_p1_restricted_permissions.png

Restricted file access denied  
screenshots/day6_p1_access_denied.png

---

## Task 2 – Process Monitoring

### Objective
Monitor running processes and identify abnormal resource usage that could indicate malicious or unauthorized activity.

### Actions Performed
- Viewed all running processes on the system
- Observed CPU and memory usage in real time
- Simulated suspicious behavior by creating a high CPU–consuming process
- Identified and terminated the abnormal process

### Commands Used
- ps aux
- top

### Evidence
Process list overview  
screenshots/day6_p2_ps_aux_output.png

Live process monitoring  
screenshots/day6_p2_top_showing_processes.png

High CPU usage detected  
screenshots/day6_p2_high_cpu_process.png

---

## Task 3 – Log Locations & Authentication Events

### Objective
Investigate Linux authentication logs to identify successful and failed login attempts from external systems.

### Actions Performed
- Simulated SSH login attempts from Kali Linux
- Simulated SSH login attempts from Windows 10
- Generated both failed and successful authentication events
- Investigated system authentication logs using the system journal

### Commands Used
- journalctl

### Evidence
SSH login attempts from external systems  
screenshots/day6_p3_ssh_login_attempts.png

Authentication events recorded in system logs  
screenshots/day6_p3_login_attempt_recorded.png

---

## Defender Takeaways
- Linux enforces security through users, ownership, and permissions
- Least privilege prevents unauthorized access to sensitive files
- Process monitoring helps identify abnormal or malicious behavior
- Authentication attempts are logged and traceable
- Logs provide critical evidence during security investigations

---

## Skills Demonstrated
- Linux user and permission management
- File ownership and permission control
- Process monitoring and anomaly detection
- Authentication log investigation
- SOC-style defensive analysis
