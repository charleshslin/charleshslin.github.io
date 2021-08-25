---
layout: single
title:  "The TL;DR of CISA's Ransomware Guide"
date:   2021-08-24 15:32:31 -0400
categories: jekyll update
---

<br>
CISA offers a ransomware guide on ransomware best practices and recommendations. Here is the TL;DR on it.

**What is ransomware?**

First of all, ransomware is a form of malware that encrypts files on a system and then demands payment in exchange for decryption. In recent years, ransomware has become increasingly prevalent.

**Best practices for ransomware prevention**

* Maintain regular, offline, encrypted backups of datas and systems and regularly test these backups
* Conduct regular vulnerability scans and remediate findings
* Regularly patch and update software and operating systems
* Ensure there is no security misconfiguration
* Employ security best practices of RDP and other remote desktop services
* Disable/block SMB outbound and remove/disable outdated SMB versions (v1 and v2)
* Mitigate against phishing
* Prevent malware using antivirus/anti-malware software, application whitelisting, and IDS
* Manage security of third-parties and managed security providers
* Employ MFA for all services possible and follow principle of least privilege
* Ensure cloud services are following security best practices
* Have strong understanding of network and employe network segmentation
* Ensure proper asset management strategy is present
* Restrict usage of PowerShell to users
* Secure domain controllers (e.g. regular patching, limit installed software/agents, prevent internet access using firewalls, follow principle of least privilege, use Kerberos, require SMB signing, etc.)
* Collect, retain, secure, and monitor logs

**Ransomware response checklist**

* Determine which systems were impacted and isolate them
* If you are unable to disconnect devices from the network, power them down
* Triage impacted systems for recovery
* Develop and document initial understanding with the response team
* Engage internal and external stakeholders
* Take system image and memory capture of a sample of affected devices and collect relevant logs
* Consult federal law enforcement
* Research trusted guidance and take appropriate action, such as killing execution of known ransomware binaries
* Identify systems and accounts involved in initial breach, including email accounts
* Contain associated systems that may be used for lateral movement
* Examine existing detection/prevention systems
* Conduct extended analysis to identify outside-in and inside-out persistence mechanisms
* Prioritize critical services and rebuild systems
* Address security gaps
* Declare ransomware incident over
* Reconnect systems and restore data
* Document lessons learned
* Share lessons learned

Remember that paying ransom will not ensure that your data will be decrypted, and you may still be compromised. CISA, MS-ISAC, and federal law enforcement do not recommend paying ransom in the event of a ransomware incident.

<a href="https://www.cisa.gov/sites/default/files/publications/CISA_MS-ISAC_Ransomware%20Guide_S508C_.pdf">https://www.cisa.gov/sites/default/files/publications/CISA_MS-ISAC_Ransomware%20Guide_S508C_.pdf</a>
