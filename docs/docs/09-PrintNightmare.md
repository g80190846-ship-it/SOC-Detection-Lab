## Objective

Simulate the PrintNightmare vulnerability to observe how Wazuh detects suspicious Print Spooler activity, executable drops, and malicious DLL creation.

---

## Attack Overview

PrintNightmare (CVE-2021-34527) is a Windows Print Spooler vulnerability that allows attackers to execute code with SYSTEM privileges. In this lab, the attack was simulated in a controlled environment to verify that Wazuh successfully detected indicators associated with the exploit.

---

## Lab Environment

| Component | Technology |
|-----------|------------|
| SIEM | Wazuh |
| Endpoint | Windows 11 |
| Attacker Machine | Kali Linux |
| Monitoring | Sysmon + Windows Event Logs |

---

## Attack Execution

1. Executed the PrintNightmare exploit in the lab environment.
2. The Windows Print Spooler attempted to load a malicious DLL.
3. Executable files were dropped into the Windows directory.
4. Wazuh collected Sysmon and Windows Event Logs.
5. Security alerts were generated and investigated through the Wazuh Threat Hunting dashboard.

---

## Wazuh Detection

### Alerts Generated

| Rule ID | Detection |
|---------|-----------|
| **92206** | DLL file created by printer spooler service (Possible PrintNightmare exploit) |
| **92217** | Executable dropped in Windows root folder |
| **92021** | PowerShell used to delete files or directories |

---

## MITRE ATT&CK Mapping

| Technique | ATT&CK ID |
|-----------|-----------|
| Exploitation for Privilege Escalation | T1068 |
| DLL Side-Loading | T1574 |
| PowerShell | T1059.001 |
| Indicator Removal on Host | T1070 |

---

## Evidence

### Wazuh Threat Hunting Alerts

![PrintNightmare Detection](../images/printnightmare/wazuh-alerts.png)

**Observed Indicators**

- DLL created by the Windows Print Spooler service.
- Executable dropped into the Windows directory.
- PowerShell activity detected during cleanup.
- Multiple correlated Wazuh alerts generated for the attack.

---

## SOC Investigation

**Severity:** High

### Findings

- Suspicious DLL creation by the Print Spooler service.
- Executable dropped into a sensitive Windows directory.
- PowerShell execution observed after exploitation.
- Multiple detections correlated to a potential privilege escalation attack.

### Recommended Response

- Isolate the affected endpoint.
- Stop the Print Spooler service if exploitation is confirmed.
- Remove malicious DLLs and dropped executables.
- Apply Microsoft security patches.
- Perform endpoint malware scanning.
- Review Sysmon and PowerShell logs for additional indicators.

---

## Outcome

The PrintNightmare simulation successfully demonstrated Wazuh's capability to detect suspicious Print Spooler activity, malicious DLL creation, executable drops, and PowerShell execution. The generated alerts enabled effective investigation and incident response within the SOC environment
