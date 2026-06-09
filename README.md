# Adversary-Emulation-Detection-Lab
## The Infrastructure Setup
### Lab Network Diagram :
<img width="1024" height="572" alt="image" src="https://github.com/user-attachments/assets/551ec9e8-3bd9-4399-b162-8c68fb2c198e" />
Windows Server = Victim machine

This is where attacks will happen. But these are controlled lab attacks using Atomic Red Team, not real-world attacks.

Sysmon = CCTV camera inside Windows

Sysmon records detailed Windows activities such as process creation, registry modification, network connection, and process access.

Splunk Universal Forwarder = Courier

It collects Windows/Sysmon logs and sends them to Splunk.

Kali/Ubuntu = SOC/SIEM machine

Splunk Enterprise runs here. It receives logs from Windows and lets you search/detect attacks.

Atomic Red Team = Attack simulator

It runs known MITRE ATT&CK technique tests, such as scheduled task creation, MSHTA execution, LSASS access, PowerShell download, and registry modification.

### Kali Configuration:
<img width="1918" height="1198" alt="Screenshot 2026-06-09 152630" src="https://github.com/user-attachments/assets/e819c4a4-4ade-470d-afa3-bec4de66b05e" />

I have assigned 4 GB RAM, 80.1 GB SSD, and 4 cores in the Kali Machine
