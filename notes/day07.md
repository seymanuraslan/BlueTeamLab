# Day 07: Logs Flowing into the SIEM

**Date:** 2026 October 11

## Goal
Send DC01 and WS01 logs to Wazuh and find events from a single place.

## What I did
* Logged in to the Wazuh dashboard from my host through port forwarding
* Installed Wazuh agents on DC01 and WS01 using the Deploy new agent wizard
* Installed the WS01 agent with adm.mehmet because a normal user cannot install software
* Generated failed logons on WS01 and searched for 4625 in Wazuh
* Added a user to a group and searched for 4728 and 4729 in Wazuh

## What I saw
* When I added a user to a group, Wazuh showed a 4728 alert. The member was shown as a SID instead of a name.

## What I learned
* Agents register on port 1515 and send logs on port 1514.
* Without a SIEM, finding failed logons on 2,000 machines would mean checking every machine one by one, and attackers can delete local logs. A SIEM keeps a central copy and lets me search all machines at once.
* In 4625, the important field is targetUserName. Many attempts on one account means brute force; one attempt on many accounts from the same IP means password spraying.
* Every new user is added to Domain Users automatically, so giving a permission to Domain Users means giving it to everyone.

## Next
Enable advanced audit policy, command line logging and PowerShell logging with a GPO.
