# Attack 10 – SSH Brute Force Detection

## Objective

Simulate an SSH brute force attack against a Linux system and verify that Wazuh detects repeated authentication failures, successful logins, and privilege escalation activities.

---

## Attack Overview

An SSH brute force attack attempts to gain unauthorized access by repeatedly trying different usernames and passwords. This simulation generated multiple failed login attempts before a successful authentication to demonstrate Wazuh's monitoring and alerting capabilities.

---

## Lab Environment

| Component | Technology |
|-----------|------------|
| SIEM | Wazuh |
| Attacker Machine | Kali Linux |
| Target Machine | Ubuntu Linux |
| Monitoring | Syslog + Wazuh Agent |

---

## Attack Flow

### Step 1 – Port Enumeration

The attacker verified that the SSH service was accessible on the target using Nmap.

**Evidence**

![Nmap Scan](../images/ssh-bruteforce/nmap-scan.png)

---

### Step 2 – SSH Login Attempts

Multiple SSH login attempts were performed using invalid usernames and passwords to simulate a brute force attack.

**Evidence**

![SSH Attack](../images/ssh-bruteforce/attack-execution.png)

---

### Step 3 – Wazuh Detection

The Wazuh agent collected Syslog and PAM authentication events and generated alerts for the failed login attempts.

**Evidence**

![Wazuh Detection](../images/ssh-bruteforce/wazuh-alerts.png)

---

### Step 4 – SOC Investigation

The generated alerts were investigated through the Wazuh Threat Hunting dashboard.

**Observed Indicators**

- Multiple failed SSH login attempts.
- Invalid username authentication.
- PAM authentication failures.
- Successful SSH login.
- Privilege escalation using `sudo`.

---

## Wazuh Detection

| Rule ID | Detection |
|---------|-----------|
| 5710 | SSH login attempt using a non-existent user |
| 2502 | Multiple incorrect password attempts |
| 5503 | PAM login failed |
| 5501 | PAM session opened |
| 5502 | PAM session closed |
| 5402 | Successful sudo command executed |

---

## MITRE ATT&CK Mapping

| Technique | ATT&CK ID |
|-----------|-----------|
| Brute Force | T1110 |
| Valid Accounts | T1078 |
| Remote Services (SSH) | T1021.004 |
| Account Discovery | T1087 |

---

## Recommended Response

- Block the attacker's IP address.
- Enable Multi-Factor Authentication (MFA).
- Disable password authentication and use SSH keys.
- Configure account lockout policies.
- Review SSH logs and sudo activity.
- Continue monitoring for repeated authentication failures.

---

## Outcome

The attack successfully demonstrated Wazuh's ability to detect SSH brute force attempts, monitor authentication events, and provide actionable alerts for SOC investigation and incident response.
