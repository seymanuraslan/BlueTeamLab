# Day 03: Creating the lab.local Domain

**Date:** 2026 October 06

## Goal
Promote DC01 to the first domain controller of a new forest, lab.local, and set up DNS the way it is done in enterprise networks.

## What I did
* Verified connectivity with hostname, ipconfig and ping before making any changes
* Installed the Active Directory Domain Services role
* Promoted DC01 to a domain controller for a new forest: lab.local, NetBIOS name LAB
* Installed DNS as part of the promotion and set a separate DSRM password
* Configured DNS forwarders 8.8.8.8 and 1.1.1.1 and removed the alternate external DNS from the network settings
* Verified name resolution with nslookup for both lab.local and google.com
* Ran dcdiag to check domain controller health
* Took a snapshot after AD DS installation

## What I saw
* When I ran dcdiag, the DC health check tool, I got many errors. I checked the timestamps and saw they were all from the moment the server rebooted after promotion, so they were expected noise from a new domain controller, not a real problem.
* When I ran nslookup google.com, the answer came back as forcesafesearch.google.com instead of the normal Google address. Something between my lab and 8.8.8.8, probably my ISP or home router, is rewriting DNS answers to force SafeSearch. I confirmed this by querying 8.8.8.8 and 1.1.1.1 directly from my host and got the same rewritten answer. This is a live example of DNS filtering.

## What I learned
* A domain can have more than one DC, but one DC can only serve one domain.
* DNS forwarders matter because domain clients send all DNS queries to the DC instead of going to public DNS directly. This gives us visibility into which sites users try to reach, and lets us block malicious domains from a single point.
* Standard DNS is not encrypted, so anyone on the path can see and even change the answers. That is how DNS filtering works, and attackers can use the same technique for DNS hijacking.

## Next
Build an OU structure, create users and groups that mimic a real company, and take a first look at security logs.
