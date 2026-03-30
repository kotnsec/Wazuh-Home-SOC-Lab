# Wazuh Installation

This section documents the installation of the Wazuh server, including the deployment process, dashboard access, and issues encountered during setup.

## Installation Method

Wazuh was installed on an Ubuntu Desktop virtual machine using the official Wazuh installation script.

The following command was used:

```bash
curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh
sudo bash wazuh-install.sh -a

```
The -a flag installs all Wazuh components:

Wazuh Manager
Wazuh Indexer
Wazuh Dashboard
Installation Process

The installation script automated the deployment of all required components. During execution, the script:

Downloaded required packages
Installed dependencies
Configured services
Generated access credentials

The process took several minutes to complete.

Accessing the Dashboard

After installation, the Wazuh dashboard was accessed through a web browser using the server's IP address:

https://<WAZUH-SERVER-IP>

Example:

https://192.168.x.x

A security warning may appear due to the use of self-signed certificates. This was expected and safely bypassed for lab purposes.

Login was performed using the credentials generated during installation.

Note: Default or generated credentials should be stored securely and never exposed in public repositories.

Services Verification

After installation, services were verified to ensure proper operation:

systemctl status wazuh-manager
systemctl status wazuh-indexer
systemctl status wazuh-dashboard

All services were confirmed to be running correctly.

Issues Encountered
1. Dashboard Not Accessible

Issue:
The Wazuh dashboard was not accessible from the browser.

Cause:
Network configuration issues related to VM connectivity.

Solution:
Switching the network mode to Bridged allowed the virtual machine to obtain a reachable IP address on the local network, resolving connectivity issues.

2. Agent Connection Delays

Issue:
The endpoint agent was not immediately connecting to the Wazuh manager.

Cause:
Initial network communication inconsistencies.

Solution:
Verified connectivity using ping and ensured both machines were on the same network segment. Restarting services resolved the issue:

sudo systemctl restart wazuh-manager
3. SSL Warning in Browser

Issue:
Browser displayed a security warning when accessing the dashboard.

Cause:
Use of self-signed certificates.

Solution:
Accepted the risk and proceeded, as this is expected behavior in lab environments.

Summary

The Wazuh installation was successfully completed using the official installation script. Despite minor networking issues, the environment was stabilized using Bridged networking, allowing proper communication between the server and endpoint.

This setup provides a fully functional SIEM environment for log analysis, detection testing, and SOC practice.
