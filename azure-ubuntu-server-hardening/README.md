# Azure Ubuntu Server Security Hardening

**Module:** Security Administration (COMP H2703) | **Academic project:** December 2025  
**Focus:** Cloud deployment, Linux administration and defence in depth

## Project overview

I deployed an Ubuntu virtual machine in Microsoft Azure and worked through several layers of security controls. The goal was to reduce exposed services, secure remote administration, monitor authentication activity, keep the operating system patched and make key configuration files recoverable.

This project was a practical system-hardening exercise, not a claim that the VM was fully production-ready.

## Technologies and concepts

Microsoft Azure Virtual Machines, Azure Virtual Networks and subnets, Network Security Groups (NSGs), Ubuntu Linux, OpenSSH, SSH keys, UFW, Fail2ban, rsyslog, logrotate, unattended-upgrades, Bash scripting and managed-disk encryption.

## What I did

1. **Provisioned a cloud network and VM.** Grouped the Azure resources and used a virtual network (`10.0.0.0/16`) with a subnet (`10.0.0.0/24`). Used NSGs to control inbound services, with SSH (22), HTTP (80) and HTTPS (443) considered for the intended workload.
2. **Hardened remote access.** Configured SSH-key authentication, disabled password authentication and direct root SSH login, and used an administrative account with `sudo` for privileged commands.
3. **Applied host firewall rules.** Enabled UFW, denied unsolicited inbound traffic by default and allowed only the selected services.
4. **Added brute-force protection.** Installed and configured Fail2ban to monitor SSH authentication failures and temporarily block repeat attempts.
5. **Improved log visibility.** Used system logging with rsyslog and logrotate to record events and manage log retention.
6. **Configured patching and backup.** Enabled unattended security updates and wrote/tested a compressed backup process for configuration files, mainly `/etc`.
7. **Worked on DNS and HTTPS.** Created DNS records for the VM, but the planned HTTPS setup was **not completed** due to DNS propagation delays. This is an explicitly documented limitation.

## How I checked the work

- Reviewed SSH daemon settings showing password authentication and root SSH login disabled.
- Checked UFW status and the list of permitted ports.
- Captured Fail2ban service/status and logging output.
- Reviewed unattended-upgrades output and described tests of the local backup script.

## Outcome and lessons

The report documents a VM with layered network and host-level security controls. I learned how cloud NSGs and operating-system controls complement each other, and why visibility, patching and recovery matter alongside firewall rules.

**Limitations:** HTTPS was not finished; the backup copies remained on the VM rather than off-site; these were class/lab checks, not a penetration test or independent proof of full security. The report does **not** substantiate Filebeat deployment, so Filebeat is deliberately not listed as project work.

## My contribution

I worked on deploying, configuring and checking the cloud VM/security controls and documented the design choices, implementation and problems encountered in my Security Administration report.

## Evidence

- [Selected, sanitised pages from my Azure project report](evidence/sanitised-report-excerpts.pdf)
- [SSH configuration evidence](evidence/ssh-hardening.png)
- [UFW firewall configuration evidence](evidence/ufw-firewall.png)

**Evidence note:** A public-sharing excerpt is provided instead of the raw coursework PDF because the original includes an assessment coversheet, Azure subscription/resource identifiers, a domain and server IP information. Relevant pages were selected and identifying parts omitted. No live credentials or private keys are supplied.
