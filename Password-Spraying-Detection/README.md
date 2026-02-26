<img width="1212" height="742" alt="splunk-password-spraying-results" src="https://github.com/user-attachments/assets/93cfea97-1ebf-476f-8837-f81b17f8bb80" />
## Password Spraying Detection – Splunk Lab

## 📌 Scenario

Multiple authentication attempts were detected across several user accounts using a limited set of passwords. This behavior may indicate a password spraying attack.

## 🛠 Lab Environment

- Splunk Enterprise
- Windows Event Logs (Security Logs)
- Event IDs monitored: 4624, 4625

## 🔎 Detection Logic

Password spraying typically:
- Targets many accounts
- Uses a small number of passwords
- Generates multiple failed logins across different usernames

## 💻 SPL Query Used

```spl
index=security EventCode=4625
| stats count by Account_Name, src_ip
| where count > 5
| sort - count
```

## 📊 Findings
- Multiple accounts targeted from a single source IP
- High volume of failed logins
- No corresponding successful authentication events

## 🚨 Response Actions
- Identified affected accounts
- Forced password reset
- Recommended MFA enforcement
- Monitored for additional activity

## 🎯 SOC Learning Outcome
- Built detection logic in Splunk
- Understood difference between brute force and password spraying
- Practiced log correlation and threshold detection**
