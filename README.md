# Firezone VPN Deployment with Ansible

This repository provides an automated solution for deploying a self-hosted VPN using Firezone, leveraging Ansible for infrastructure as code (IaC). Firezone is an intuitive, lightweight, and performant VPN platform built upon WireGuard.

---

## Overview

Firezone simplifies VPN management by offering:

* **Fast and secure connectivity** using WireGuard.
* **Intuitive UI** for managing users, devices, and access controls.
* **Minimal infrastructure overhead**, suitable for small teams, labs, or personal projects.

This Ansible playbook helps automate the provisioning and setup of Firezone quickly and reliably.

---

## Prerequisites

Before running this playbook, ensure you have:

* A Linux server (tested on Ubuntu).
* Ansible installed on your local machine.

  ```bash
  sudo apt update && sudo apt install ansible -y
  ```
* Install Docker with all the packages. [Ubuntu Installation](https://docs.docker.com/engine/install/ubuntu/#:~:text=and%20development%20environments.-,Install%20using%20the,repository,-Before%20you%20install)
* SSH key-based authentication set up to access your target host.

---

## Repository Structure

```
firezone-vpn/
├── ansible.cfg       # Ansible configuration file
├── hosts.ini         # Inventory defining the local host
└── run_firezone.yaml # Main Ansible playbook
```

---

## Configuration

### Step 1: Update Inventory

Your `hosts.ini` is pre-configured for local execution, no changes are needed unless you deviate from a local deployment:

```ini
[local]
localhost ansible_connection=local
```

### Step 2: Adjust Firezone Site Name

Set your desired Firezone UI domain name by modifying the variable `firezone_sitename` within the playbook.

---

## Running the Playbook

Execute the playbook directly on your local VM:

```bash
git clone https://github.com/kapilll/firezone-vpn.git
cd firezone-vpn
sudo ansible-playbook -i hosts.ini run_firezone.yaml
```

This will:

* Install necessary dependencies.
* Set up Docker containers for WireGuard and Firezone.
* Configure Nginx reverse proxy for handling web traffic.
* Configure firewall rules and SSL certificates.
* Launch the Firezone application.

---

## Accessing Firezone

After successful deployment, access the Firezone UI via your web browser using your configured site name:

```
https://your_firezone_sitename
```

Default login details will be outputted during the playbook execution or can be set via environment variables in the playbook.

---

## Troubleshooting

If deployment fails, ensure:

* Docker is installed and functioning correctly.
* Nginx is configured correctly to proxy Firezone's Docker container.
* SSL certificates are correctly issued and valid.
* Firewall rules permit required VPN and HTTP(S) traffic.

---

## Contributions

Pull requests and suggestions for improvement are welcome! Feel free to open issues or submit contributions to enhance this project.
