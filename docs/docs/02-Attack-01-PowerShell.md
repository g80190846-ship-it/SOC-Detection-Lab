# Attack 01 – PowerShell Execution

## Objective
Simulate suspicious PowerShell execution and verify detection using Wazuh SIEM.

## Attack

Executed PowerShell with hidden window and command-line arguments to simulate malicious execution.

## Detection

- Wazuh Rule: 92005
- Alert: PowerShell process created an executable in Windows root folder

## MITRE ATT&CK

- T1059.001 – PowerShell

## Investigation

Reviewed process creation events in Wazuh Threat Hunting, validated PowerShell command-line activity, and confirmed successful detection.

## Outcome

The attack was successfully detected and investigated through Wazuh.
