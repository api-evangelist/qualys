---
title: "RefluXFS: A Linux Kernel Local Privilege Escalation to Root in XFS (CVE-2026-64600)"
url: "https://blog.qualys.com/vulnerabilities-threat-research/2026/07/22/refluxfs-a-linux-kernel-local-privilege-escalation-to-root-in-xfs-cve-2026-64600"
date: "2026-07-22"
author: "Saeed Abbasi"
feed_url: "https://blog.qualys.com/feed"
---
Executive summary Qualys Threat Research Unit (TRU) identified CVE-2026-64600, a race condition in the Linux kernel’s XFS filesystem copy-on-write path. An attacker with an ordinary local account can exploit this race condition to overwrite protected files on disk and gain host root privileges on affected systems, including deployments running SELinux in Enforcing mode. This discovery […]
