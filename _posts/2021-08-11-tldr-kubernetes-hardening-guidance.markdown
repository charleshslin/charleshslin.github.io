---
layout: single
title:  "The TL;DR of CISA and NSA's Kubernetes Hardening Guidance"
date:   2021-08-10 15:32:31 -0400
categories: jekyll update
---

<br>
On August 3, 2021, the NSA and CISA released a cyber security technical report, “Kubernetes Hardening Guidance.” Here is the TL;DR of it:

The three common sources of compromise in Kubernetes are supply chain risks, malicious threat actors, and insider threats.

High-level recommended mitigations include the following:
* Scan containers and Pods for vulnerabilities or misconfigurations
* Run containers and Pods with the least privileges possible
* Use network separation to control the amount of damage a compromise can cause
* Use firewalls to limit unneeded network connectivity and encryption to protect confidentiality
* Use strong authentication and authorization to limit user and administrator access as well as to limit the attack surface
* Use log auditing so that administrators can monitor activity and be alerted to potential malicious activity
* Periodically review all Kubernetes settings and use vulnerability scans to help ensure risks are appropriately accounted for and security patches are applied

The slightly more detailed version of that:
* Kubernetes Pod security
	* Use containers built to run applications as non-root users
	* Where possible, run containers with immutable file systems
	* Scan container images for possible vulnerabilities or misconfigurations
	* Use a Pod Security Policy to enforce a minimum level of security including:
		* Preventing privileged containers
		* Denying container features frequently exploited to breakout, such as hostPID, hostIPC, hostNetwork, allowedHostPath
		* Rejecting containers that execute as the root user or allow elevation to root
		* Hardening applications against exploitation using security services such as SELinux®, AppArmor®, and seccomp
* Network separation and hardening
	* Lock down access to control plane nodes using a firewall and role-based access control (RBAC)
	* Further limit access to the Kubernetes etcd server
	* Configure control plane components to use authenticated, encrypted communications using Transport Layer Security (TLS) certificates
	* Set up network policies to isolate resources. Pods and services in different namespaces can still communicate with each other unless additional separation is enforced, such as network policies
	* Place all credentials and sensitive information in Kubernetes Secrets rather than in configuration files. Encrypt Secrets using a strong encryption method
* Authentication and authorization
	* Disable anonymous login (enabled by default)
	* Use strong user authentication
	* Create RBAC policies to limit administrator, user, and service account activity
* Log auditing
	* Enable audit logging (disabled by default)
	* Persist logs to ensure availability in the case of node, Pod, or container level failure
	* Configure a metrics logger
* Upgrading and application security practices
	* Immediately apply security patches and updates
	* Perform periodic vulnerability scans and penetration tests
	* Remove components from the environment when they are no longer needed

The report also goes into more detail for each one of these and is quite comprehensive and laid out detailedly. [Check it out!][guidance]

[guidance]: https://media.defense.gov/2021/Aug/03/2002820425/-1/-1/1/CTR_KUBERNETES%20HARDENING%20GUIDANCE.PDF


