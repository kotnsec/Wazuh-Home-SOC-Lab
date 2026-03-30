# Wazuh-Home-SOC-Lab
This project documents the creation of a home SOC lab using VMware, Ubuntu Desktop, Ubuntu Server, and Wazuh. The objective was to simulate a basic enterprise monitoring environment, connect an endpoint to the SIEM, and prepare the lab for attack detection and incident analysis.
## Objectives
- Build a functional SIEM lab using Wazuh
- Deploy a monitored Linux endpoint
- Validate network communication between systems
- Prepare the environment for threat detection use cases
- Document setup, troubleshooting, and future detection scenarios
## Technologies Used
- VMware Workstation
- Ubuntu Desktop
- Ubuntu Server
- Wazuh
- Linux networking
  SSH## Lab Architecture
- Wazuh Server: Ubuntu Desktop VM
- Endpoint/Victim Machine: Ubuntu Server VM
- Hypervisor: VMware Workstation
- Network mode: NAT
## Current Status
- Wazuh server installed and accessible via dashboard
- Linux endpoint deployed
- Agent connected successfully to the Wazuh manager
- Lab ready for detection testing and attack simulation
## Next Steps
- Simulate SSH brute-force attacks
- Simulate Nmap reconnaissance
- Capture alerts and investigate logs
- Create incident-style writeups
