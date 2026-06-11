<img width="1917" height="1197" alt="nice two" src="https://github.com/user-attachments/assets/beee634f-11bb-458b-be6b-1d0ca4d649ee" />
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

<img width="1918" height="1198" alt="Screenshot 2026-06-09 163850" src="https://github.com/user-attachments/assets/7c6d7088-5b44-4ca1-85d1-e050897b026d" />

<img width="1917" height="1198" alt="Screenshot 2026-06-09 163917" src="https://github.com/user-attachments/assets/d70a7269-974e-410f-a7de-1c496ec6e1a9" />

<img width="1918" height="1198" alt="Screenshot 2026-06-09 165149" src="https://github.com/user-attachments/assets/5555317f-6038-41b7-be59-259105f55ff3" />

<img width="1918" height="1198" alt="Screenshot 2026-06-09 165728" src="https://github.com/user-attachments/assets/b3cff205-0580-4a2b-ac2a-dc4bd8a5580e" />

<img width="1917" height="1198" alt="Screenshot 2026-06-09 165810" src="https://github.com/user-attachments/assets/c4c8fd71-aa6b-434f-bc23-5446acca7a38" />

### Splunk Enterprise Installation on KALI Machine:

#### Step-1

First, we need to download Splunk Enterprise to the Kali Machine using the wget -O command.
<img width="1918" height="1198" alt="Splunk Enterprise Download" src="https://github.com/user-attachments/assets/c58476ce-b0b3-4c26-8edf-a1318d73b9af" />

#### Step-2

After that, we need to install it on our Kali Machine using the dpkg -i command.
<img width="1918" height="1198" alt="installing Splunk on Kali" src="https://github.com/user-attachments/assets/9301ceec-84ad-47b4-8a69-73c4d2887698" />

#### Step-3

Then we need to start Splunk Enterprise on our machine using sudo /opt/splunk/bin/splunk start --accept-license --run-as-root command.
<img width="1917" height="1197" alt="starting splunk on kali" src="https://github.com/user-attachments/assets/8deae633-f6a8-48b2-98e7-7e62d5795c90" />

#### Step-4

Open Splunk Enterprise on the browser.
<img width="1917" height="1197" alt="Splunk opening on browser" src="https://github.com/user-attachments/assets/655b4ebd-36fc-42be-9085-860c8437e10f" />
<img width="1917" height="1197" alt="Splunk Dashboard" src="https://github.com/user-attachments/assets/f73345f8-9f57-42ea-a60f-d545009cf745" />

#### Step-5

Set the receiving port to 9997.
<img width="1917" height="1195" alt="setting recieving port on Splunk Enterprise" src="https://github.com/user-attachments/assets/fcfce050-c1dd-4cc0-a413-c6cfd863753a" />



### Sysmon Installation on Windows Server 2019

#### Step-1

At first, we need to download Sysmon and the Sysmon config file on our machine by using PowerShell.

<img width="1915" height="1191" alt="Sysmon download and unzipped on server" src="https://github.com/user-attachments/assets/174dc969-86d2-419c-b3d1-ebb48f1d4682" />
<img width="1917" height="1197" alt="download sysmon configuration file" src="https://github.com/user-attachments/assets/2de282a9-d626-42c0-ae60-1c632f86fdc8" />


#### Step-2
After that, we need to install it.
<img width="1917" height="1195" alt="Installed Sysmon" src="https://github.com/user-attachments/assets/6457fe32-443c-4177-a789-263cdef94e87" />

#### Step-3
Check if the Sysmon is running or not.
<img width="1917" height="1197" alt="Check service if sysmon is running or not" src="https://github.com/user-attachments/assets/0aab7662-571b-4ba3-a447-2744cad2ed2a" />
<img width="1917" height="1197" alt="Sysmon checking on Event viewer if running or not" src="https://github.com/user-attachments/assets/d273751b-bc7a-45f4-bcaf-4103816dd7d0" />

### Splunk Universal Forwarder Installation:

##### At first, we have to again check the IP address and make sure that the Splunk Enterprise port is accessible from the Windows server. As I restarted my main machine, my IP address of Kali got changed to 192.168.214.130, and I have also checked from the Windows server if the port is accessible or not.


<img width="1917" height="1197" alt="port checking" src="https://github.com/user-attachments/assets/d6ed5981-884a-4ffa-8f95-597be786f22c" />

##### Now, we are ready to install the universal forwarder on our Windows server machine.
<img width="1915" height="1197" alt="forwarder 1" src="https://github.com/user-attachments/assets/c681d0e5-d8c5-4adc-a33c-7b2fa5dd176e" />
<img width="1917" height="1197" alt="forwarder 2" src="https://github.com/user-attachments/assets/eb0d1cfa-85e0-4c1c-8209-2aa62efcddd2" />
<img width="1917" height="1197" alt="forwarder 3" src="https://github.com/user-attachments/assets/903f7228-627b-46a1-bb37-4477266842d1" />
<img width="1917" height="1197" alt="forwarder 4" src="https://github.com/user-attachments/assets/5187b855-bc1d-4d7b-a27d-4811910569dd" />

##### Now we'll check if the forwarder is active or not.
<img width="1917" height="1197" alt="forwarder 5" src="https://github.com/user-attachments/assets/fe833cd4-61fe-4f84-b87f-b3934c194ce9" />


#### Configure Universal Forwarder to collect Sysmon logs

##### Create inputs.conf inside "C:\Program Files\SplunkUniversalForwarder\etc\system\local"
<img width="1917" height="1197" alt="create input conf" src="https://github.com/user-attachments/assets/3eca4bb1-bcab-4715-baa5-a87eb3f9b182" />

<img width="1917" height="1197" alt="inputs conf 2" src="https://github.com/user-attachments/assets/ec6dc989-8c16-4f65-8c86-f08b2430c689" />

#### Restart Universal forwarder and then check the status
<img width="1917" height="1197" alt="restart forwarder" src="https://github.com/user-attachments/assets/840ac281-17dd-4c18-8986-1ac51b4f00a1" />
<img width="1917" height="1197" alt="forwarder status" src="https://github.com/user-attachments/assets/0c29248f-e997-4a7b-a485-2ecdd4d04148" />


#### Generate Test Sysmon Logs
<img width="1917" height="1197" alt="testing if sysmon can capture them or not" src="https://github.com/user-attachments/assets/0a95018b-0c02-4222-a81e-526a99425733" />


##### While I was trying to see the logs from Splunk Enterprise, I triggered a problem and couldn't see any events, then I figured out one major problem that my inputs.conf file was actually in a text format, so I fixed it.
<img width="1917" height="1197" alt="triggered problem 1" src="https://github.com/user-attachments/assets/d40066fc-f8e3-4860-8c66-e3c4914e3471" />

#### Verifying Windows Sysmon Logs in Splunk

After configuring the Splunk Universal Forwarder, I verified that Windows Server logs were successfully received by Splunk Enterprise running on Kali. First, I searched the `main` index and confirmed that logs were coming from the Windows Server host.

SPL Query:

```spl
index=main
| stats count by host source sourcetype
```

<img width="1917" height="1197" alt="nice two" src="https://github.com/user-attachments/assets/3889358b-6f64-4d57-8dc1-e15f375f171d" />







