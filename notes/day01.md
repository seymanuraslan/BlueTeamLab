# Day 01: Host Preparation and Virtualization Setup

**Date:** 2026 October 05

## Goal
Prepare the host machine and virtualization environment for a blue team home lab.

## What I did
* Checked host resources: 16 GB RAM, 4 CPU cores, 300 GB free HDD space
* Verified hardware virtualization is enabled
* Installed VirtualBox and the Extension Pack
* Created an isolated NAT Network named LabNet with subnet 10.10.10.0/24 and DHCP disabled
* Downloaded Windows Server 2025, Windows 11 Enterprise, Ubuntu Server 24.04.5 LTS and Kali Linux images
* Created this repository to document the lab

## What I saw
* Host has an HDD instead of an SSD, so I planned VM resources carefully: max three VMs running at once and dynamic disks.
* Verified the Kali image integrity with SHA256 before use.

## What I learned
* Type 1 hypervisors run directly on hardware, Type 2 run on top of a host OS.
* I chose NAT Network instead of Bridged mode so lab traffic and malware tests stay isolated from my home network, while VMs can still talk to each other.
* DHCP is disabled because servers in a real enterprise network use static IPs.

## Next
Install Windows Server 2025 as DC01 and promote it to a domain controller for lab.local.
