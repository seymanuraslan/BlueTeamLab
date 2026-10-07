# Day 04: Building LabCorp

**Date:** 2026 October 07

## Goal
Turn the empty domain into a realistic company with departments, users and groups, and see how these changes appear in the security logs.

## What I did
* Reran dcdiag to confirm the DC is healthy after the first full day
* Created the LabCorp OU structure with departments, computers, groups, admin accounts and service accounts
* Created 10 user accounts, including a separate admin account for an IT user and a service account
* Created four department security groups and assigned members
* Added the admin account to Domain Admins
* Reviewed Security logs in Event Viewer for event IDs 4720, 4728, 4624 and 4625

## What I saw
* dcdiag showed warnings again, but all of them were from the moment I started DC01. All important tests passed.
* In the 4624 logs, most entries were not from people. I saw DC01$ logging on to itself with Logon Type 3. The $ means it is a computer account. This is normal background noise and should be filtered in a SIEM.

## What I learned
* Logon Type shows how a session was opened: 2 is logging in at the machine, 3 is over the network, 7 is unlocking the screen and 10 is RDP.
* Admins should have two accounts: one for daily work and one only for admin tasks. If the daily account gets phished, the attacker still cannot get domain admin rights.

## Next
Install WS01, join it to lab.local and run a DNS sinkhole exercise.
