# ActiveDirectory


## Configuration and set up

For Windows Target and Domain Controller machine, instucting Splunk Forwarder to push events related to Application, Security, and System to splunk server.
![image](https://github.com/KennuC/ActiveDirectory/assets/131323586/b7aa0b6e-ae6f-4941-9f88-aa55feee131f)

Adding Active Directory Domain Service feature on Domain Controller machine
![image](https://github.com/KennuC/ActiveDirectory/assets/131323586/9a63f0c5-b585-435d-859e-24c8c0cececd)


Generic Names in new Organizaitonal Units IT & HR
![image](https://github.com/KennuC/ActiveDirectory/assets/131323586/c080c7fc-0de6-4ae8-a890-a5b6ea471a0a)
![image](https://github.com/KennuC/ActiveDirectory/assets/131323586/73837024-f6bf-4a5c-8c49-b13b44cf5726)

Adding Windows10Target machine onto the kennu.local Domain

![image](https://github.com/KennuC/ActiveDirectory/assets/131323586/b09fe2ee-d5f4-47ac-a014-e6e6895badd9)

Logging onto other user on Windows10Target machines shows that it will log in to the domain KENNU
![image](https://github.com/KennuC/ActiveDirectory/assets/131323586/4d961621-2743-4c6f-b1df-e3cbb59a0895)

Using crowbar on Kali to bruteforce an account on the Windows10Target machine via remote desktop with a custom password text file.
![image](https://github.com/KennuC/ActiveDirectory/assets/131323586/7ab91d2a-4206-4e01-acfd-112daaaa7b90)

Using splunk query 'index="endpoint" sourcetype="WinEventLog:Security" jsmith' and identifying the top EventCode of 4625 with 60 counts of events, after research this event is generated when a logon request fails.
![image](https://github.com/KennuC/ActiveDirectory/assets/131323586/36b960cc-326d-4574-87c3-5fd0bd8634bc)

Adding the EventCode to the search to investigate the events. Show many failed login attempts occured within a few seconds, in indication of a potential brute-force attack
![image](https://github.com/KennuC/ActiveDirectory/assets/131323586/f0e890d9-74b5-4198-9f43-44cb9ce15989)

Changing the EventCode to 4624 for successful login attempt and investigating the event show that the workstation name is under kali as well as the IP address 10.0.2.4
![image](https://github.com/KennuC/ActiveDirectory/assets/131323586/4c729ec7-a9d8-4b5b-8165-133a9a8f251b)

Using Atomic Red to replicate event logs, based on MITRE ATT&CK, selecting Command and Scripting Interpreter: PowerShell (ID: T1059.001)
![image](https://github.com/KennuC/ActiveDirectory/assets/131323586/e96ad857-6836-42ae-b50e-92bbe918dfef)

To see if the splunk server has logged this, we will search for an execute that has taken place for this instance '-exec bypass -noprofile'
![image](https://github.com/KennuC/ActiveDirectory/assets/131323586/cc77567f-ff55-496f-878e-c92940765ac2)
![image](https://github.com/KennuC/ActiveDirectory/assets/131323586/2429c5c8-53d3-401d-b6f7-8836cd3f62c3)


