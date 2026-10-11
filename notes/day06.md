# Day 06: SIEM01, Wazuh and Moving the Lab

**Date:** 2026 October 08

## Goal
Build SIEM01 on Ubuntu Server and install Wazuh as the lab SIEM.

## What I did
* Created SIEM01: Ubuntu Server 24.04.5, static IP 10.10.10.20, DNS pointing to DC01
* Extended the root LVM volume to use the full disk
* Installed Wazuh 4.14 all in one, using the command from the official Wazuh documentation
* Moved the whole lab to a 32 GB RAM laptop with an SSD using a USB drive
* Recreated LabNet and added a port forwarding rule so I can reach the Wazuh dashboard from my host at 127.0.0.1:8443

## What I saw
* By default Ubuntu used only half of the disk for the root volume. I resized it manually.
* ping replies from DC01 had TTL 128 and from the internet TTL 64. Windows starts at 128, Linux at 64, so TTL can hint at the OS.

## What I learned
* Wazuh has three parts: indexer stores logs, server analyzes them with rules, dashboard is the web interface.
* The Wazuh dashboard uses a self signed certificate, so the browser shows a warning. In real companies internal sites should use certificates from the company CA so users do not learn to ignore warnings.

## Next
Install Wazuh agents on DC01 and WS01.
