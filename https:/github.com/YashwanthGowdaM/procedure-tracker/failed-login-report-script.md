---
title: "Failed Login Report Script"
category: "Linux [Shell scripting]"
tags: ["security", "authentication", "log", "log analysis"]
lastUpdated: "2026-07-23"
status: "Fresh"
estimatedMinutes: 10
author: "Linux Engineer, Infosec, Cyber Sceurity"
version: "1.0"
summary: "Failed Login Report Script"
---

# Failed Login Report Script

## Script Name
`failed_login_report.sh`

---

## Objective
- Check whether the authentication log exists.
- Count the total number of failed SSH login attempts.
- Display the top source IP addresses.
- Display all failed login entries.
- Generate an alert if failed login attempts exceed a defined threshold.

---

## Script

```bash
#!/bin/bash

# Authentication log file
LOG_FILE="/var/log/secure"

# Alert threshold
THRESHOLD=10

# Step 1: Check if log file exists
if [ ! -f "$LOG_FILE" ]; then
    echo "ERROR: Log file not found!"
    exit 1
fi

echo "========================================"
echo "        Failed Login Report"
echo "========================================"
echo "Generated On : $(date)"
echo

# Step 2: Count failed login attempts
FAILED_COUNT=$(grep -c "Failed password" "$LOG_FILE")

echo "Step 2: Total Failed Login Attempts"
echo "Count : $FAILED_COUNT"
echo

# Step 3: Generate Alert (if threshold exceeded)
echo "Step 3: Alert Status"

if [ "$FAILED_COUNT" -gt "$THRESHOLD" ]; then
    echo "ALERT: Failed login attempts exceeded the threshold ($THRESHOLD)"
else
    echo "Status: Login attempts are within the acceptable limit."
fi

echo

# Step 4: Display Top Source IP Addresses
echo "Step 4: Top Source IP Addresses"

grep "Failed password" "$LOG_FILE" \
| awk '{print $(NF-3)}' \
| sort \
| uniq -c \
| sort -nr

echo

# Step 5: Display Failed Login Entries
echo "Step 5: Failed Login Entries"

grep "Failed password" "$LOG_FILE"

echo
echo "========== Report Completed =========="
```

---

## Sample Output

```text
========================================
        Failed Login Report
========================================
Generated On : Wed Jul 22 16:15:25 IST 2026

Step 2: Total Failed Login Attempts
Count : 18

Step 3: Alert Status
ALERT: Failed login attempts exceeded the threshold (10)

Step 4: Top Source IP Addresses

8 192.168.1.10
5 10.0.0.15
5 172.16.1.20

Step 5: Failed Login Entries

Jul 22 09:10:10 server sshd[1234]: Failed password for root from 192.168.1.10 port 55210 ssh2
Jul 22 09:11:20 server sshd[1245]: Failed password for admin from 10.0.0.15 port 55211 ssh2
...
```

---

## Commands Used

| Command | Purpose |
|---------|---------|
| `grep -c` | Count failed login attempts |
| `grep` | Display matching log entries |
| `awk` | Extract source IP addresses |
| `sort` | Sort the IP addresses |
| `uniq -c` | Count occurrences of each IP |
| `date` | Display the report generation time |
| `if` | Check conditions and generate alerts |
| `exit 1` | Exit the script if the log file is missing |

---

## Customization

Change the alert threshold:

```bash
THRESHOLD=20
```

Use the Ubuntu authentication log instead:

```bash
LOG_FILE="/var/log/auth.log"
```
