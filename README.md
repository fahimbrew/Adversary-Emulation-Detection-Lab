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
<img width="1918" height="1198" alt="Screenshot 2026-06-0https://youtube.com/9 152630" src="https://github.com/user-attachments/assets/e819c4a4-4ade-470d-afa3-bec4de66b05e" />

I have assigned 4 GB RAM, 80.1 GB SSD, and a 4-core processor in the Kali Machine.

Network Adapter on NAT.

### Windows 2019 Server Configuration:
<img width="1918" height="1198" alt="Screenshot 2026-06-09 153553" src="https://github.com/user-attachments/assets/022c7877-72ae-4b89-93c0-d5c5796de399" />

I have assigned 4 GB RAM, 20 GB SSD, and a 2-core processor in the Windows Server Machine.

Network Adapter on NAT.

### PING Test

At first, I checked the IP address for both machines, and then I tried to ping each other. When I pinged from the Windows server, I didn't face any issue but while I was trying to ping windows server from Kali machine then I encountered a problem then I have discovered that window server's defender was blocking the ping and then I fixed the issue from windows server. Now both machine can ping each other. 

<img width="1917" height="1198" alt="Screenshot 2026-06-09 165810" src="https://github.com/user-attachments/assets/c4c8fd71-aa6b-434f-bc23-5446acca7a38" />
<img width="1918" height="1198" alt="Screenshot 2026-06-09 165728" src="https://github.com/user-attachments/assets/b3cff205-0580-4a2b-ac2a-dc4bd8a5580e" />
<img width="1918" height="1198" alt="Screenshot 2026-06-09 165149" src="https://github.com/user-attachments/assets/5555317f-6038-41b7-be59-259105f55ff3" />
<img width="1917" height="1198" alt="Screenshot 2026-06-09 163917" src="https://github.com/user-attachments/assets/d70a7269-974e-410f-a7de-1c496ec6e1a9" />
<img width="1918" height="1198" alt="Screenshot 2026-06-09 163850" src="https://github.com/user-attachments/assets/7c6d7088-5b44-4ca1-85d1-e050897b026d" />



