# Day 08: Audit Policy with GPO

**Date:** 2026 October 11

## Goal
Make Windows log more events, especially process creation and PowerShell, using a GPO.

## What I did
* Created a GPO called LabCorp Audit Policy
* Turned on advanced audit settings like logon, Kerberos, account and group management and process creation
* Turned on command line logging for 4688 and PowerShell Script Block Logging for 4104
* Linked the GPO to the LabCorp OU and the Domain Controllers OU
* Ran gpupdate and checked with gpresult and auditpol
* Ran discovery commands on WS01 as Ayse, like whoami, net user /domain, net group "Domain Admins" /domain and ipconfig /all
* Found these commands in Event Viewer as 4688 and 4104 events

## What I saw
* Ayse, a normal Finance user, could list all domain accounts with one command. Names like adm.mehmet and svc.backup show attackers which accounts are important.

## What I learned
* 4688 shows every new process. With command line logging, I can see the full command.
* The Creator Process Name field shows the parent process. For example, whoami.exe was started by powershell.exe. Many detection rules look at this parent and child relation.
* 4104 shows what ran in PowerShell, even if the attacker encoded it.
* Some cmd commands like dir or echo are not separate programs, so they do not create 4688.
* If I saw net group "Domain Admins" on a Finance user's computer, I would think the account or computer may be compromised and an attacker is doing discovery.In MITRE ATT&CK, this technique is called Permission Groups Discovery. I would check the parent process, other commands at the same time, and if the user was really at the computer.

## Next
Install Sysmon to get more details like network connections, DNS queries and file hashes.
