# Troubleshooting

This section documents the main issues encountered during the setup of the Wazuh SOC homelab, along with their root causes and solutions.

The goal of this section is to demonstrate practical problem-solving and troubleshooting skills during deployment.

---

1. Endpoint Not Receiving IPv4 Address

**Issue:
The endpoint machine was not receiving a valid IPv4 address.

**Symptoms:
- No network connectivity
- `ping` failed
- `ip a` showed no assigned IPv4

**Cause:
DHCP was not properly assigning an IP address to the virtual machine.

**Solution:
- Restarted network services
- Verified network adapter configuration in VMware
- Ensured the VM was connected using **Bridged mode**

After switching to Bridged networking, the machine successfully obtained an IPv4 address.

---

2. DHCP and Network Configuration Issues

**Issue
Unstable or inconsistent IP assignment.

**Symptoms:
- Changing IP addresses
- Intermittent connectivity issues

**Cause:
Misconfiguration of virtual network settings and DHCP behavior.

**Solution:
- Confirmed both VMs were connected to the same network adapter
- Ensured consistent Bridged configuration
- Verified network interface settings inside the OS

---

3. DNS Resolving to IPv6 Instead of IPv4

**Issue:
DNS queries were resolving to IPv6 addresses, causing connectivity issues.

**Symptoms:
- Failed connections despite valid domain resolution
- Unexpected IPv6 addresses in responses

**Cause:
System preferred IPv6 over IPv4.

**Solution:
- Verified DNS resolution using:

```bash
ping google.com
Forced IPv4 testing when needed:
ping -4 google.com
Focused communication using direct IPv4 addresses for lab setup
4. Wazuh Agent Download Failure
```

Issue:
The Wazuh agent package could not be downloaded.

**Symptoms:

curl failed to retrieve the file
Connection errors

**Cause:
Network or DNS issues affecting external connectivity.

**Solution:

Verified internet access using ping
Checked DNS resolutio
Retried download after network stabilization

---
4. Agent Not Connecting to Manager

**Issue:
The Wazuh agent did not connect to the manager.

**Symptoms:

Agent not appearing in dashboard
No logs received

**Cause:
Incorrect IP address configured in the agent.

**Solution:

Verified manager IP address
Updated configuration file:
sudo nano /var/ossec/etc/ossec.conf
Restarted agent service:
sudo systemctl restart wazuh-agent
---
5. Confusion Between Manager and Endpoint IPs

**Issue:
Incorrect identification of which IP belonged to the server vs the endpoint.

**Symptoms:

Failed agent enrollment
Connectivity errors

**Cause:
Lack of clear mapping between virtual machines.

**Solution:

Used the following command on each VM:
ip a
Documented IP addresses for each system
Clearly labeled roles (Manager vs Endpoint)
---
6. Dashboard Not Accessible

**Issue:
Unable to access the Wazuh dashboard via browser.

**Symptoms:

Browser timeout
Connection refused

**Cause:
Network isolation when using NAT mode.

**Solution:

Switched both VMs to Bridged networking
Verified connectivity with ping
Successfully accessed dashboard using server IP
Key Takeaways
Network configuration is critical in virtualized environments
Bridged mode provided more reliable communication than NAT in this lab
Verifying connectivity (ping, ip a, logs) is essential before troubleshooting applications
Clear identification of roles (server vs endpoint) prevents configuration errors
---

***This troubleshooting process strengthened understanding of networking, system configuration, and SIEM deployment in a controlled lab environment.***
