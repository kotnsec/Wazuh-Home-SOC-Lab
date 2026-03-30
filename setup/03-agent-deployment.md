# Agent Deployment

This section documents the deployment of the Wazuh agent on a Linux endpoint, including enrollment, connectivity validation, and verification of agent status.

## Agent Installation

The Wazuh agent was installed on an Ubuntu Server virtual machine using the official Wazuh repository.

The following commands were executed:

```bash
curl -sO https://packages.wazuh.com/4.x/wazuh-agent_4.x_amd64.deb
sudo dpkg -i wazuh-agent_4.x_amd64.deb
Agent Configuration
```

After installation, the agent was configured to communicate with the Wazuh manager.

The configuration file was edited:

sudo nano /var/ossec/etc/ossec.conf

The manager IP address was defined:

<client>
  <server>
    <address>WAZUH-SERVER-IP</address>
  </server>
</client>
Agent Enrollment

The agent was registered with the Wazuh manager using the authentication tool:

sudo /var/ossec/bin/agent-auth -m WAZUH-SERVER-IP

This step allowed the agent to securely enroll with the manager.

Starting the Agent

Once configured and enrolled, the agent service was started:

sudo systemctl enable wazuh-agent
sudo systemctl start wazuh-agent
Verifying Agent Status
On the Endpoint

The agent status was verified locally:

sudo systemctl status wazuh-agent

The service was confirmed to be active and running.

On the Wazuh Server

The agent was verified from the manager:

sudo /var/ossec/bin/agent_control -l

The agent appeared in the list with an Active status.

Additionally, the agent was visible in the Wazuh Dashboard under the agents section.

Connectivity Verification

Connectivity between the endpoint and the Wazuh server was validated using:

ping WAZUH-SERVER-IP

Successful responses confirmed network reachability.

Additionally, logs confirmed communication between agent and manager:

sudo tail -f /var/ossec/logs/ossec.log

Log entries showed successful registration and data transmission.

Issues Encountered
1. Agent Not Appearing in Dashboard

Issue:
The agent was not visible in the Wazuh dashboard after installation.

Cause:
Incorrect server IP configuration.

Solution:
Updated the correct manager IP in the agent configuration file and restarted the service:

sudo systemctl restart wazuh-agent
2. Connectivity Problems

Issue:
The agent could not communicate with the server.

Cause:
Network configuration issues between virtual machines.

Solution:
Ensured both machines were using Bridged networking, allowing them to communicate within the same local network.

Summary

The Wazuh agent was successfully deployed and connected to the Wazuh manager. Proper connectivity was verified through system commands, log inspection, and dashboard visibility.

This setup enables real-time monitoring of endpoint activity and serves as the foundation for detection and analysis use cases in the SOC homelab.
