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
index=main (Sysmon OR notepad.exe OR calc.exe OR whoami OR ipconfig)
| table _time host source sourcetype _raw
```

<img width="1917" height="1197" alt="nice two" src="https://github.com/user-attachments/assets/3889358b-6f64-4d57-8dc1-e15f375f171d" />

#### Now I will install the Splunk Add-on for Sysmon.
<img width="1917" height="1197" alt="Splunk Add-on for Sysmon install" src="https://github.com/user-attachments/assets/0f7e6576-c2b8-4527-9bd2-147116e8bc4f" />

##### I am now creating a new index on Splunk Enterprise named 'win' and from the server side, I will update the inputs.conf file.
<img width="1917" height="1192" alt="creating new index" src="https://github.com/user-attachments/assets/f59a7b63-4173-44e4-a4f8-92586869af59" />
<img width="1917" height="1197" alt="creating new index input on server" src="https://github.com/user-attachments/assets/79c11aaf-5f3d-416d-95df-235d7454513b" />


##### Checked on Kali Machine
<img width="1917" height="1197" alt="checked on Kali" src="https://github.com/user-attachments/assets/143570c8-ed91-4ddb-9b13-cefd06ea0029" />


### Invoke-AtomicRedTeam Installation

#### Windows Defender Interference

During Atomic Red Team setup, Windows Defender detected some Atomic Red Team components as suspicious because the framework contains attack-simulation scripts. Since this was an isolated lab VM, I added exclusions for the Atomic Red Team folder and temporarily disabled real-time protection only during installation/testing.


<img width="1917" height="1197" alt="invokeredteam 1" src="https://github.com/user-attachments/assets/4cb4af56-f454-4961-b44c-4f5843aed327" />
<img width="1917" height="1197" alt="invokeredteam 2" src="https://github.com/user-attachments/assets/8b90869c-1f9a-42b8-8594-011ca79e1956" />
<img width="1917" height="1197" alt="invokeredteam 3" src="https://github.com/user-attachments/assets/c176f404-65fe-40d6-b9f3-4cc5b321f982" />
<img width="1917" height="1197" alt="invokeredteam 4" src="https://github.com/user-attachments/assets/b6b369b0-a5ad-4b76-9eae-b0827c37c325" />
<img width="1917" height="1197" alt="invokeredteam 5 test" src="https://github.com/user-attachments/assets/33ef065c-f24a-4415-9ee3-d3d304f59a08" />

##### Finally, I tested if it is working or not


## Red Team Attack


### Attack 1: T1053.005 - Scheduled Task

For the first attack, I selected Atomic Red Team test number 8 under T1053.005. This test imports an XML scheduled task with a hidden attribute. Attackers use scheduled tasks to maintain persistence because the task can run automatically at a defined time or trigger.

PowerShell Command:

```powershell
Invoke-AtomicTest T1053.005 -showDetailsBrief
Invoke-AtomicTest T1053.005 -TestNumbers 8 -GetPrereqs
Invoke-AtomicTest T1053.005 -TestNumbers 8
```

<img width="1917" height="1197" alt="Test 1 (1)" src="https://github.com/user-attachments/assets/a7123797-4705-463c-90af-b8743ab581d1" />

### Attack 2: T1218.005 - MSHTA

For the second attack, I selected Atomic Red Team test number 3 under T1218.005. This test is named Mshta Executes Remote HTML Application (HTA). The purpose of this test is to abuse mshta.exe, a legitimate Microsoft-signed Windows binary, to execute a remote HTA file. Attackers may use this technique to execute malicious script content while bypassing some application control or security restrictions.

PowerShell Command:

```powershell
Invoke-AtomicTest T1218.005 -TestNumbers 3 -GetPrereqs
Invoke-AtomicTest T1218.005 -TestNumbers 3
```
<img width="1917" height="1197" alt="Test 2" src="https://github.com/user-attachments/assets/6396729e-77db-40db-8998-f2ca10d9c9ea" />


### Attack 3: T1003.001 - LSASS Dumping

For the third attack, I selected Atomic Red Team test number 1 under T1003.001. This test simulates LSASS memory dumping using ProcDump. Attackers often target lsass.exe because LSASS stores authentication-related information in memory.

PowerShell Command:

```powershell
Invoke-AtomicTest T1003.001 -ShowDetailsBrief
Invoke-AtomicTest T1003.001 -TestNumbers 1 -GetPrereqs
Invoke-AtomicTest T1003.001 -TestNumbers 1
```

<img width="1917" height="1197" alt="test 3 1" src="https://github.com/user-attachments/assets/3748ccc2-95b4-492e-8f24-d85fa200e944" />
<img width="1917" height="1197" alt="test 3 2" src="https://github.com/user-attachments/assets/66d89efd-fec6-45a9-bad5-310c1ce1e9b7" />

### Attack 4: T1059.001 - PowerShell

For the fourth attack, I selected Atomic Red Team test number 6 under `T1059.001`. This test uses PowerShell with an MSXML COM object. Attackers commonly abuse PowerShell because it is built into Windows and can be used to execute commands, download content, or run scripts.

PowerShell is a trusted Windows tool, so malicious PowerShell activity can sometimes blend in with normal administrative activity. That is why command-line logging and Sysmon process creation logs are important for detecting this technique.

PowerShell Command:

```powershell
Invoke-AtomicTest T1059.001 -ShowDetailsBrief
Invoke-AtomicTest T1059.001 -TestNumbers 6 -GetPrereqs
Invoke-AtomicTest T1059.001 -TestNumbers 6
```

<img width="1917" height="1197" alt="Test 4" src="https://github.com/user-attachments/assets/02c56ca7-3aaa-49a3-a192-569fac28622a" />


### Attack 5: T1112 - Registry Modification

For the fifth attack, I selected multiple Atomic Red Team tests under `T1112`: test numbers `38`, `51`, and `56`. These tests simulate registry modification and Windows Defender-related configuration changes. Attackers may modify registry keys or security settings to weaken protection, hide activity, or perform defense evasion.

The selected Atomic tests were:

* `T1112-38` - Suppress Windows Defender Notifications
* `T1112-51` - Disable Windows Defender Notification
* `T1112-56` - Tamper Windows Defender Protection

PowerShell Command:

```powershell
Invoke-AtomicTest T1112 -TestNumbers 38,51,56 -GetPrereqs
Invoke-AtomicTest T1112 -TestNumbers 38,51,56
```

During execution, test numbers `38` and `51` completed successfully with exit code `0`. Test number `56` returned an `Access is denied` message with exit code `1`. This means the tamper protection test was attempted but was blocked by system permissions or protection restrictions. Even though test `56` did not fully completed, it still generated useful activity for investigation because it showed an attempted security-related configuration change.

<img width="1917" height="1197" alt="Attack 5 1" src="https://github.com/user-attachments/assets/010e1433-4cc0-47c6-bb97-8b7b11d49bc4" />
<img width="1917" height="1197" alt="Attack 5 2" src="https://github.com/user-attachments/assets/4ec938cd-7cef-4328-a83a-491633168b3f" />
<img width="1917" height="1197" alt="Attack 5 3 trial" src="https://github.com/user-attachments/assets/b59ae697-c6f6-4b1f-988b-f6f815a8f00b" />




## Blue Team

### Detection 1: T1053.005 (Persistence) | Scheduled Task

After executing the Atomic Red Team test for `T1053.005`, I started the blue team detection phase in Splunk. The goal of this detection was to identify scheduled task creation behavior from Windows Sysmon logs.

This attack was detected by searching for Task Scheduler-related activity, especially `schtasks.exe`, `Task Scheduler`, `Schedule.Service`, and hidden scheduled task behavior. These indicators are useful because attackers commonly use scheduled tasks to maintain persistence on a compromised Windows system.

#### SPL Query

```spl
index=win source="WinEventLog:Microsoft-Windows-Sysmon/Operational" ("schtasks.exe" OR "Task Scheduler" OR "Schedule.Service" OR "Hidden")
| rex field=_raw "<EventID[^>]*>(?<EventCode>\d+)</EventID>"
| rex field=_raw "<Data Name='UtcTime'>(?<UtcTime>[^<]+)</Data>"
| rex field=_raw "<Data Name='Image'>(?<ProcessName>[^<]+)</Data>"
| rex field=_raw "<Data Name='CommandLine'>(?<CommandLine>[^<]+)</Data>"
| table _time UtcTime host EventCode ProcessName CommandLine
```

#### Detection Explanation

The Splunk query searched the `win` index, where Windows Server Sysmon logs were forwarded. I filtered the Sysmon Operational logs for scheduled task related indicators such as `schtasks.exe`, `Task Scheduler`, and `Schedule.Service`.

The query extracted important fields from the raw XML log, including:

* `EventCode`
* `UtcTime`
* `ProcessName`
* `CommandLine`

This helped prove the required detection evidence: the time of execution, the process involved, and the command line used during the scheduled task activity.

#### Most Helpful Sysmon Event ID

The most helpful Sysmon Event ID for this detection was:

```text
Sysmon Event ID 1 - Process Creation
```

Sysmon Event ID 1 was useful because it records newly created processes along with the full command line. This allowed me to identify the scheduled task creation behavior and confirm that the Atomic Red Team test generated observable Windows activity.

#### Result

The Splunk result showed scheduled task-related activity from the Windows Server. The detection output included the event time, host name, Sysmon Event ID, process name, and command line. This confirms that the blue team was able to detect the `T1053.005` persistence technique using Sysmon logs in Splunk.

<img width="1917" height="1197" alt="Detection 1" src="https://github.com/user-attachments/assets/6931e232-686b-4566-8ae6-faef12db3664" />


### Detection 2: T1218.005 (Defense Evasion) | MSHTA

After executing the Atomic Red Team test for T1218.005, I searched Splunk for suspicious MSHTA execution. The detection focused on mshta.exe, HTA file execution, and script-related command-line activity.

```spl
index=win source="WinEventLog:Microsoft-Windows-Sysmon/Operational"
| rex field=_raw "<EventID[^>]*>(?<EventCode>\d+)</EventID>"
| rex field=_raw "<Data Name='UtcTime'>(?<UtcTime>[^<]+)</Data>"
| rex field=_raw "<Data Name='Image'>(?<ProcessName>[^<]+)</Data>"
| rex field=_raw "<Data Name='CommandLine'>(?<CommandLine>[^<]+)</Data>"
| eval cmd=lower(coalesce(CommandLine,"")), proc=lower(coalesce(ProcessName,""))
| where EventCode="1" AND (like(proc,"%mshta.exe%") OR like(cmd,"%mshta%") OR like(cmd,"%.hta%") OR like(cmd,"%javascript:%") OR like(cmd,"%vbscript:%"))
| table _time UtcTime host EventCode ProcessName CommandLine
```

#### Most Helpful Sysmon Event ID
Sysmon Event ID 1 - Process Creation

Sysmon Event ID 1 was most helpful because it records newly created processes and their full command lines. This allowed me to identify mshta.exe execution and confirm that the Atomic Red Team test generated observable Windows activity.

#### Result

The Splunk result showed MSHTA-related activity from the Windows Server. The output included time, host, Event ID, process name, and command line, confirming that the blue team was able to detect the T1218.005 defense evasion technique.

<img width="1917" height="1197" alt="Detection 2" src="https://github.com/user-attachments/assets/65818bf7-ffbc-4957-83f6-2df3dbf294bf" />


### Detection 3: T1003.001 (Credential Access) | LSASS Dumping

After executing the Atomic Red Team test for `T1003.001`, I searched Splunk for LSASS dumping behavior. This test used ProcDump to dump the memory of `lsass.exe`. Since LSASS stores authentication-related information in memory, attackers commonly target it for credential access.

The goal of this detection was to identify suspicious use of `procdump.exe` and command-line activity related to `lsass.exe`.

#### SPL Query

```spl
index=win source="WinEventLog:Microsoft-Windows-Sysmon/Operational"
| rex field=_raw "<EventID[^>]*>(?<EventCode>\d+)</EventID>"
| rex field=_raw "<Data Name='UtcTime'>(?<UtcTime>[^<]+)</Data>"
| rex field=_raw "<Data Name='Image'>(?<Image>[^<]+)</Data>"
| rex field=_raw "<Data Name='CommandLine'>(?<CommandLine>[^<]+)</Data>"
| rex field=_raw "<Data Name='SourceImage'>(?<SourceImage>[^<]+)</Data>"
| rex field=_raw "<Data Name='TargetImage'>(?<TargetImage>[^<]+)</Data>"
| rex field=_raw "<Data Name='GrantedAccess'>(?<GrantedAccess>[^<]+)</Data>"
| eval cmd=lower(coalesce(CommandLine,"")), image=lower(coalesce(Image,"")), source=lower(coalesce(SourceImage,"")), target=lower(coalesce(TargetImage,""))
| where (EventCode="1" AND (like(image,"%procdump%") OR like(cmd,"%procdump%") OR like(cmd,"%lsass%"))) OR (EventCode="10" AND like(target,"%lsass.exe%"))
| eval ProcessName=coalesce(Image,SourceImage)
| table _time UtcTime host EventCode ProcessName CommandLine SourceImage TargetImage GrantedAccess

```
#### Detection Explanation

The Splunk query searched the win index, where Windows Sysmon logs were forwarded. The query extracted important fields from the raw XML Sysmon logs, including EventCode, UtcTime, ProcessName, CommandLine, SourceImage, TargetImage, and GrantedAccess.

In the detection result, Splunk showed command-line activity where procdump.exe was used against lsass.exe and created a dump file named lsass_dump.dmp. This is strong evidence of LSASS dumping behavior.

Most Helpful Sysmon Event ID
Sysmon Event ID 1 - Process Creation

Sysmon Event ID 1 was most visible in my result because it captured the process execution and full command line. The command line clearly showed procdump.exe being used to dump lsass.exe.

Sysmon Event ID 10 - Process Access

Sysmon Event ID 10 is also very useful for LSASS dumping detection because it can show when one process accesses lsass.exe. However, in my screenshot, the clearest evidence came from Event ID 1 process creation logs.

#### Result

The Splunk result showed LSASS dumping activity from the Windows Server. The output included the event time, host name, Sysmon Event ID, process name, and command line. The command line showed procdump.exe being used to dump lsass.exe, confirming that the blue team was able to detect the T1003.001 credential access technique.

<img width="1917" height="1197" alt="detection 3 on trial" src="https://github.com/user-attachments/assets/4a26caea-fa33-428f-afcc-1c1a92eb165c" />


### Detection 4: T1059.001 (Execution) | PowerShell

After executing the Atomic Red Team test for `T1059.001`, I searched Splunk for suspicious PowerShell execution. The goal of this detection was to identify PowerShell command-line activity involving MSXML, remote content retrieval, and script execution.

This test used PowerShell with the `Msxml2.ServerXmlHttp` COM object to request remote content from GitHub and execute the response using `IEX`. This behavior is suspicious because attackers commonly use PowerShell to download and execute scripts from remote sources.

#### SPL Query

```spl
index=win source="WinEventLog:Microsoft-Windows-Sysmon/Operational"
| rex field=_raw "<EventID[^>]*>(?<EventCode>\d+)</EventID>"
| rex field=_raw "<Data Name='UtcTime'>(?<UtcTime>[^<]+)</Data>"
| rex field=_raw "<Data Name='Image'>(?<ProcessName>[^<]+)</Data>"
| rex field=_raw "<Data Name='CommandLine'>(?<CommandLine>[^<]+)</Data>"
| eval cmd=lower(coalesce(CommandLine,"")), proc=lower(coalesce(ProcessName,""))
| where EventCode="1" AND (like(proc,"%powershell%") OR like(cmd,"%powershell%"))
| where like(cmd,"%msxml%") OR like(cmd,"%xmlhttp%") OR like(cmd,"%serverxmlhttp%") OR like(cmd,"%iex%") OR like(cmd,"%invoke-expression%") OR like(cmd,"%invoke-webrequest%") OR like(cmd,"%http%")
| table _time UtcTime host EventCode ProcessName CommandLine
```

#### Detection Explanation

The Splunk query searched the `win` index, where Windows Server Sysmon logs were forwarded. The query extracted important fields from the raw XML Sysmon logs, including `EventCode`, `UtcTime`, `ProcessName`, and `CommandLine`.

The detection result showed PowerShell execution with suspicious command-line indicators such as `Msxml2.ServerXmlHttp`, `GET`, a GitHub URL, and `IEX`. This indicates that PowerShell was used to retrieve remote content and execute it, which matches the behavior of the Atomic Red Team test for `T1059.001`.

This helped prove the required detection evidence: execution time, process name, and command line.

#### Most Helpful Sysmon Event ID

```text
Sysmon Event ID 1 - Process Creation
```

Sysmon Event ID 1 was the most helpful event because it captured the PowerShell process and the full command line. The command line clearly showed PowerShell using `Msxml2.ServerXmlHttp` to request remote content and execute it with `IEX`.

```text
Sysmon Event ID 3 - Network Connection
```

Sysmon Event ID 3 can also be useful for this technique because it can show outbound network connections made by PowerShell. However, in this detection screenshot, the clearest evidence came from Event ID 1 process creation logs.

#### Result

The Splunk result showed PowerShell-related activity from the Windows Server. The output included event time, host name, Sysmon Event ID, process name, and command line. The command line showed PowerShell using `Msxml2.ServerXmlHttp`, a remote GitHub URL, and `IEX`, confirming that the blue team was able to detect the `T1059.001` execution technique using Sysmon logs in Splunk.

<img width="1917" height="1197" alt="detection 4 on trial 2" src="https://github.com/user-attachments/assets/72cb0f54-1c9c-4806-9abb-8802a6654555" />


### Detection 5: T1112 (Defense Evasion) | Registry Modification

After executing the Atomic Red Team tests for `T1112`, I searched Splunk for registry modification and Windows Defender related configuration changes. The goal of this detection was to identify registry value changes, Defender notification changes, and tamper protection modification attempts from Sysmon logs.

This detection focused on Sysmon registry events and process creation events related to `reg.exe`, `cmd.exe`, Windows Defender registry paths, notification settings, and tamper protection settings.

#### SPL Query

```spl
index=win source="WinEventLog:Microsoft-Windows-Sysmon/Operational"
| rex field=_raw "<EventID[^>]*>(?<EventCode>\d+)</EventID>"
| rex field=_raw "<Data Name='UtcTime'>(?<UtcTime>[^<]+)</Data>"
| rex field=_raw "<Data Name='Image'>(?<ProcessName>[^<]+)</Data>"
| rex field=_raw "<Data Name='CommandLine'>(?<CommandLine>[^<]+)</Data>"
| rex field=_raw "<Data Name='TargetObject'>(?<RegistryPath>[^<]+)</Data>"
| rex field=_raw "<Data Name='Details'>(?<Details>[^<]+)</Data>"
| eval cmd=lower(coalesce(CommandLine,"")), proc=lower(coalesce(ProcessName,"")), reg=lower(coalesce(RegistryPath,"")), details=lower(coalesce(Details,""))
| where EventCode IN ("1","12","13","14") AND (
    like(cmd,"%defender%") OR like(cmd,"%notification%") OR like(cmd,"%tamper%") OR like(cmd,"%set-itemproperty%") OR like(cmd,"%new-itemproperty%") OR like(cmd,"%reg add%") OR
    like(reg,"%defender%") OR like(reg,"%notification%") OR like(reg,"%tamper%") OR like(reg,"%security center%") OR
    like(details,"%disable%") OR like(details,"%dword%")
)
| table _time UtcTime host EventCode ProcessName CommandLine RegistryPath Details
```

#### Detection Explanation

The Splunk query searched the `win` index, where Windows Server Sysmon logs were forwarded. The query extracted important fields from the raw Sysmon XML logs, including `EventCode`, `UtcTime`, `ProcessName`, `CommandLine`, `RegistryPath`, and `Details`.

The query searched for Defender and registry-related indicators such as:

* `defender`
* `notification`
* `tamper`
* `reg add`
* `set-itemproperty`
* `new-itemproperty`
* `dword`
* Defender-related registry paths

In the detection result, Splunk showed registry modification activity involving Windows Defender settings. The results included commands such as `reg add` and registry values such as `TamperProtection`, `DisableNotifications`, and `Notification_Suppress`. This is useful evidence because attackers may modify registry values to weaken security settings or hide security notifications.

This helped prove the required detection evidence: time of execution, process name, command line, registry path, and registry modification details.

#### Most Helpful Sysmon Event ID

```text
Sysmon Event ID 13 - Registry Value Set
```

Sysmon Event ID 13 was the most helpful event because it records registry value modification. In this detection, Event ID 13 showed registry paths related to Windows Defender configuration changes.

```text
Sysmon Event ID 1 - Process Creation
```

Sysmon Event ID 1 was also useful because it captured the process and command line used to make the registry changes. In the result, processes such as `reg.exe` and `cmd.exe` were visible with command lines showing Defender-related registry modification.

#### Result

The Splunk result showed registry and Windows Defender related activity from the Windows Server. The output included event time, host name, Sysmon Event ID, process name, command line, registry path, and registry details.

The result showed `reg.exe` and `cmd.exe` being used to modify Defender-related registry values such as `TamperProtection`, `DisableNotifications`, and `Notification_Suppress`. This confirms that the blue team was able to detect the `T1112` registry modification and defense evasion technique using Sysmon logs in Splunk.

<img width="1917" height="1197" alt="detection 5 1 main" src="https://github.com/user-attachments/assets/34424520-2bfe-40f4-bf1e-55ee2d90c789" />
<img width="1917" height="1197" alt="detection 5 2 main" src="https://github.com/user-attachments/assets/393d315a-56bb-4a97-b886-56005ee32109" />
<img width="1917" height="1197" alt="detection 5 3 main" src="https://github.com/user-attachments/assets/671c627b-bb6e-402d-9301-d2c39037dbad" />

Note: Test numbers 38 and 51 completed successfully with exit code `0`. Test number 56 returned `Access is denied` with exit code `1`, meaning the tamper protection modification was attempted but blocked by system protection or permissions. The attempted command still generated useful logs for blue team detection.




---

## Key Skills Demonstrated

This project demonstrates practical hands-on experience in both red team emulation and blue team detection engineering. The lab covered the complete workflow of building a small SOC-style detection environment, generating realistic attacker-like activity, collecting endpoint telemetry, and writing SPL queries to identify suspicious behavior.

Key skills demonstrated in this project include:

* Windows Server 2019 security monitoring
* Kali Linux based Splunk Enterprise deployment
* Splunk Universal Forwarder configuration
* Sysmon installation and event collection
* Windows Event Log forwarding
* Custom Splunk index creation
* Atomic Red Team adversary emulation
* MITRE ATT&CK technique mapping
* SPL query writing and field extraction
* Detection of process creation, process access, registry modification, and suspicious command-line activity
* Troubleshooting real lab issues such as network connectivity, Defender blocking, missing dependencies, and incorrect file formats

---

## Conclusion

In this project, I successfully built an end-to-end adversary emulation and detection lab using Windows Server 2019, Kali Linux, Splunk Enterprise, Sysmon, Splunk Universal Forwarder, and Atomic Red Team. The Windows Server acted as the victim endpoint, while Kali Linux hosted Splunk Enterprise as the SIEM platform. Sysmon was used to collect detailed endpoint telemetry, and the Splunk Universal Forwarder was configured to send Windows and Sysmon logs into a dedicated Splunk index named `win`.

After completing the logging pipeline, I used Atomic Red Team to emulate five MITRE ATT&CK techniques in a controlled lab environment. These techniques included scheduled task persistence, MSHTA abuse, LSASS dumping, PowerShell execution, and registry modification. Each attack was executed on the Windows Server and then investigated from the blue team side using Splunk.

The detection phase focused on identifying real technical behavior rather than simply searching for the word “Atomic.” For each attack, I wrote SPL queries that extracted important fields such as event time, process name, command line, registry path, source process, target process, and access rights. This helped prove that the attacks were visible in the collected telemetry and could be investigated by a security analyst.

The most useful Sysmon events in this lab were Event ID 1 for process creation, Event ID 10 for process access, Event ID 13 for registry value modification, and Event ID 3 for network connection activity. These events provided strong visibility into attacker-like behavior such as `schtasks.exe` execution, `mshta.exe` abuse, `procdump.exe` dumping `lsass.exe`, PowerShell downloading and executing remote content, and registry changes related to Windows Defender settings.

This project improved my understanding of how attackers use legitimate Windows tools for persistence, defense evasion, credential access, execution, and registry modification. More importantly, it showed how defenders can use endpoint logs, Sysmon telemetry, and Splunk SPL queries to detect those behaviors.

From a SOC analyst and detection engineering perspective, this lab demonstrates my ability to build a detection environment, troubleshoot log ingestion problems, emulate adversary behavior safely, investigate endpoint activity, and create meaningful detections mapped to MITRE ATT&CK. It also reflects practical skills that are directly relevant to security monitoring, threat hunting, incident response, and blue team operations.

Overall, this lab helped me connect red team activity with blue team visibility. It shows that effective detection is not only about collecting logs, but also about understanding attacker behavior, selecting the right telemetry, writing accurate queries, and clearly explaining the evidence found during investigation.














