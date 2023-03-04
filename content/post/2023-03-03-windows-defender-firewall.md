---
author: Tristan Madden
categories: [CMD]
date: 2023-03-03
tags: [netsh, firewall]
title: Windows Defender Firewall
summary: Examples of rules are commonly used in network setups where specific programs or ports need to be allowed through the firewall to ensure that they can communicate with other devices or software.
---

<h2>Firewall Rules</h2>

<h3>Turn the firewall on or off</h3>

```CMD
netsh advfirewall set allprofiles state on
netsh advfirewall set allprofiles state off
```
<h3>Exception for a program</h3>
This example allows incoming traffic for the program "WaspPunch.exe" located at "C:\Program Files (x86)\Wasp Technologies\WaspTime\WaspPunch.exe". The "dir=in" parameter specifies that the rule applies to inbound traffic. The "action=allow" parameter allows the traffic through, and "enable=yes" ensures that the rule is enabled.

```CMD
netsh advfirewall firewall add rule name="WaspPunch.exe" dir=in action=allow program="C:\Program Files (x86)\Wasp Technologies\WaspTime\WaspPunch.exe" enable=yes
```

<h3>Exception for a port</h3>
These rules allow incoming TCP traffic on ports 10004 and 10005. Again, the "dir=in" parameter specifies that the rules apply to inbound traffic, "action=allow" allows the traffic through, and "enable=yes" ensures that the rules are enabled.

```CMD
netsh advfirewall firewall add rule name="10004" dir=in action=allow protocol=TCP localport=10004 enable=yes
netsh advfirewall firewall add rule name="10005" dir=in action=allow protocol=TCP localport=10005 enable=yes
```