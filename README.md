# Active Directory Attack

## Objective

The Active Directory Attack project aims to create a realistic environment for simulating and detecting cyber attacks within an Active Directory infrastructure. The primary focus is to utilize various tools and techniques to monitor, detect, and analyze attack patterns, improving overall network security knowledge and defensive strategies.


### Skills Learned

- Advanced understanding of Active Directory configurations and security implications.
- Proficiency in using SIEM systems (like Splunk) for log ingestion and analysis.
- Capability to perform network analysis using tools such as Wireshark.
- Expertise in recognizing and responding to attack signatures and patterns.
- Enhanced knowledge of network protocols, security vulnerabilities, and mitigation techniques.
- Development of critical thinking and problem-solving skills in cybersecurity.

### Tools Used

- **Splunk**: For log ingestion and real-time analysis of security events.
- **Kali Linux**: For using Crowbar to brute-force through remote desktop.
- **Atomic Red Team**: For simulating adversary techniques based on the MITRE ATT&CK framework.
- **VirtualBox**: For setting up virtual machines to create a controlled lab environment.
- **Domain Controller**: Windows Server 2022 for active directory.
- **Sysmon**: For for system monitoring logs that will be forwarded to splunk.

## Network Diagram

![NetworkDiagram](https://github.com/KennuC/ActiveDirectoryAttack/assets/131323586/90e3e58a-e85e-4940-bbd0-199265f30282)

*Ref 1: Network Diagram*

## Steps

### Configuring Splunk Forwarder on Windows Target and Domain Controller

Instructing the Splunk Forwarder to push events related to Application, Security, and System logs to the Splunk server.
![Splunk Forwarder Configuration](https://github.com/KennuC/ActiveDirectory/assets/131323586/b7aa0b6e-ae6f-4941-9f88-aa55feee131f)
*Ref 2: Splunk Forwarder Configuration*

### Adding Active Directory Domain Services

Setting up the Active Directory Domain Services feature on the Domain Controller machine.
![Active Directory Setup](https://github.com/KennuC/ActiveDirectory/assets/131323586/9a63f0c5-b585-435d-859e-24c8c0cececd)
*Ref 3: Active Directory Setup*

### Creating Organizational Units

Creating new Organizational Units (OUs) named IT and HR with generic names for users.
![Organizational Units - IT & HR](https://github.com/KennuC/ActiveDirectory/assets/131323586/c080c7fc-0de6-4ae8-a890-a5b6ea471a0a)
*Ref 4: Organizational Units - IT & HR*
![Organizational Units - IT & HR](https://github.com/KennuC/ActiveDirectory/assets/131323586/73837024-f6bf-4a5c-8c49-b13b44cf5726)
*Ref 5: Organizational Units - IT & HR (Cont.)*

### Adding Windows10Target to the Domain

Joining the Windows 10 Target machine to the `kennu.local` domain.
![Windows 10 Domain Join](https://github.com/KennuC/ActiveDirectory/assets/131323586/b09fe2ee-d5f4-47ac-a014-e6e6895badd9)

*Ref 6: Windows 10 Domain Join*

### Domain Login Verification

Logging in to a different user account on the Windows 10 Target machine to verify domain integration.
![Domain Login Verification](https://github.com/KennuC/ActiveDirectory/assets/131323586/4d961621-2743-4c6f-b1df-e3cbb59a0895)
*Ref 7: Domain Login Verification*

### Brute-force Attack Simulation Using Crowbar

Using Crowbar on Kali Linux to brute-force an account on the Windows 10 Target machine via Remote Desktop with a custom password list.
![Crowbar Brute-force Attack](https://github.com/KennuC/ActiveDirectory/assets/131323586/7ab91d2a-4206-4e01-acfd-112daaaa7b90)

*Ref 8: Crowbar Brute-force Attack*

### Analyzing Failed Login Attempts in Splunk

Using the Splunk query `index="endpoint" sourcetype="WinEventLog:Security" jsmith` to identify EventCode 4625, indicating failed login attempts.
![Failed Login Attempts Analysis](https://github.com/KennuC/ActiveDirectory/assets/131323586/36b960cc-326d-4574-87c3-5fd0bd8634bc)
*Ref 9: Failed Login Attempts Analysis*

### Investigating Brute-force Attack Patterns

Adding EventCode 4625 to the search to investigate multiple failed login attempts, indicating a potential brute-force attack.
![Brute-force Attack Investigation](https://github.com/KennuC/ActiveDirectory/assets/131323586/f0e890d9-74b5-4198-9f43-44cb9ce15989)
*Ref 10: Brute-force Attack Investigation*

### Analyzing Successful Login Attempts

Changing the EventCode to 4624 to investigate successful login attempts, revealing the attacker’s IP address and workstation name.
![Successful Login Analysis](https://github.com/KennuC/ActiveDirectory/assets/131323586/4c729ec7-a9d8-4b5b-8165-133a9a8f251b)
*Ref 11: Successful Login Analysis*

### Simulating Attack Techniques Using Atomic Red Team

Using Atomic Red Team to replicate event logs based on MITRE ATT&CK, focusing on PowerShell execution (ID: T1059.001).
![Atomic Red Team Simulation](https://github.com/KennuC/ActiveDirectory/assets/131323586/e96ad857-6836-42ae-b50e-92bbe918dfef)
*Ref 12: Atomic Red Team Simulation*

### Verifying Attack Simulations in Splunk

Searching for specific PowerShell execution patterns in Splunk to verify logging and detection.
![PowerShell Execution Logging](https://github.com/KennuC/ActiveDirectory/assets/131323586/cc77567f-ff55-496f-878e-c92940765ac2)
*Ref 13: PowerShell Execution Logging*
![PowerShell Execution Logging](https://github.com/KennuC/ActiveDirectory/assets/131323586/2429c5c8-53d3-401d-b6f7-8836cd3f62c3)
*Ref 14: PowerShell Execution Logging (Cont.)*


