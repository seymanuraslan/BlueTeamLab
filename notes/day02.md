# Day 02: Building DC01

**Date:** 2026 October 05

## Goal
Install Windows Server 2025 as the future domain controller DC01.

## What I did
* Created DC01 VM: 3 GB RAM, 2 vCPU, 50 GB dynamic disk, attached to LabNet
* Disabled unattended installation to go through every setup screen manually
* Installed Windows Server 2025 Standard Evaluation with Desktop Experience
* Installed VirtualBox Guest Additions
* Added Turkish Q keyboard layout
* Set time zone to Istanbul, static IP 10.10.10.10/24 with gateway 10.10.10.1, and renamed the host to DC01
* Took a clean snapshot before installing AD DS

## What I saw
* I realized the keyboard was set to US, so I changed it to Turkish Q. I kept US as a backup because my password was set with it.

## What I learned
* Microsoft recommends Server Core instead of Desktop Experience, because it has a smaller attack surface. Fewer components means fewer vulnerabilities and fewer patches.
* I learned that malware often checks whether it is running in a virtual environment or sandbox. To detect this, it looks for signs like the VBoxService process, low RAM, or MAC addresses that belong to VirtualBox.

## Next
Verify connectivity, install AD DS and promote DC01 to a domain controller for lab.local.
