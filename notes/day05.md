# Day 05: WS01 and the First Domain Member

**Date:** 2026 October 08

## Goal
Build the first employee workstation, WS01, join it to lab.local and test a DNS sinkhole.

## What I did
* Created WS01 VM: 4 GB RAM, 2 vCPU, 64 GB dynamic disk, EFI, Secure Boot and TPM 2.0, attached to LabNet
* Installed Windows 11 Enterprise Evaluation with a local account
* Set static IP 10.10.10.101 with DNS pointing to DC01
* Joined WS01 to lab.local using the separate admin account adm.mehmet
* Logged in to WS01 as LAB\ayse.yilmaz
* Reviewed 4741, 4768 and 4624 events on DC01
* Created a DNS sinkhole for testmalware.com on DC01 and tested it from WS01
* Took snapshots of both VMs

## What I saw
* I found two 4741 events. One was WS01$ created by adm.mehmet when I joined the domain. The other was DC01$ created by ANONYMOUS LOGON when I built the domain. During setup this is normal, but in a running domain an anonymous logon creating a computer account would be a serious alert.
* In the 4768 event for Ayse, the service name was krbtgt and RC4 was in the available keys.

## What I learned
* Sinkhole means sending a malicious domain to a fake address in DNS, so nobody can reach it. testmalware.com returned 127.0.0.1 from DC01.
* But when I asked 8.8.8.8 directly from WS01, I got the real IP addresses. So a sinkhole only works if all clients use the company DNS. Companies should block outbound port 53 for everything except the DCs.
* krbtgt is the account that signs all Kerberos tickets. If an attacker steals its hash, they can create fake tickets. This is called Golden Ticket.

## Next
Install Ubuntu Server on SIEM01 and set up Wazuh.
