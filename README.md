# Wazuh Installation and Setup Guide (SIEM + XDR) on Linux

This guide explains how to install and configure **Wazuh**, an open-source **SIEM and XDR platform**, for cybersecurity monitoring and SOC lab environments.

Wazuh provides:

* Log analysis
* Intrusion detection
* File integrity monitoring
* Vulnerability detection
* Security event monitoring

This setup installs:

* Wazuh Manager
* Wazuh Indexer
* Wazuh Dashboard

---

# System Requirements

Recommended minimum system requirements:

| Resource | Requirement                      |
| -------- | -------------------------------- |
| CPU      | 4 cores                          |
| RAM      | 8 GB                             |
| Disk     | 50–100 GB                        |
| OS       | Ubuntu 22.04 / CentOS 7 / Debian |
| Internet | Required                         |

For lab environments you can run it inside:

* VMware
* VirtualBox
* Cloud VM

---

# Step 1 — Update the System

Update system packages before installation.

```bash id="h1k8o2"
sudo apt update && sudo apt upgrade -y
```

For CentOS systems:

```bash id="s6t10f"
sudo yum update -y
```

---

# Step 2 — Install Required Tools

Install basic utilities.

```bash id="j2d7la"
sudo apt install curl wget tar -y
```

---

# Step 3 — Download Wazuh Installation Script

Wazuh provides an automated installation script.

Official documentation:

https://documentation.wazuh.com/current/installation-guide/index.html

Download the installer:

```bash id="q4p1kx"
curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh
```

Make the script executable:

```bash id="7q2g3w"
chmod +x wazuh-install.sh
```

---

# Step 4 — Install Wazuh (All-in-One Deployment)

Run the installer for a single-node deployment.

```bash id="t9r5c1"
sudo ./wazuh-install.sh -a
```

This will install:

* Wazuh Manager
* Wazuh Indexer
* Wazuh Dashboard

Installation takes **10–20 minutes** depending on system resources.

---

# Step 5 — Retrieve Dashboard Credentials

After installation completes, the installer generates login credentials.

To view them:

```bash id="c5p7e2"
sudo tar -O -xvf wazuh-install-files.tar wazuh-install-files/wazuh-passwords.txt
```

Example output:

```
Username: admin
Password: ********
```

Save these credentials.

---

# Step 6 — Access the Wazuh Dashboard

Find your system IP address:

```bash id="r6g8n4"
ip a
```

Example:

```
192.168.56.101
```

Open the dashboard in your browser:

```
https://<YOUR-IP>
```

Example:

```
https://192.168.56.101
```

---

# Step 7 — Login to Wazuh

Use the credentials generated during installation.

Example:

```
Username: admin
Password: ********
```

You should now see the **Wazuh Security Dashboard**.

---

# Step 8 — Verify Wazuh Services

Check if Wazuh services are running.

Manager:

```bash id="k1c9r8"
sudo systemctl status wazuh-manager
```

Indexer:

```bash id="o3f6a2"
sudo systemctl status wazuh-indexer
```

Dashboard:

```bash id="x9v2q5"
sudo systemctl status wazuh-dashboard
```

---

# Restart Wazuh After Power Off

If the system shuts down or restarts, start the services again.

Start Manager:

```bash id="d2n6y3"
sudo systemctl start wazuh-manager
```

Start Indexer:

```bash id="m7a1q9"
sudo systemctl start wazuh-indexer
```

Start Dashboard:

```bash id="p5k8w4"
sudo systemctl start wazuh-dashboard
```

---

# Restart All Wazuh Services

```bash id="v8b4s6"
sudo systemctl restart wazuh-manager
sudo systemctl restart wazuh-indexer
sudo systemctl restart wazuh-dashboard
```

---

# Stop Wazuh Services

```bash id="g1u3f8"
sudo systemctl stop wazuh-manager
sudo systemctl stop wazuh-indexer
sudo systemctl stop wazuh-dashboard
```

---

# Check Service Status

```bash id="h8x2d7"
sudo systemctl status wazuh-manager
```

---

# Adding Agents to Wazuh

Agents allow you to monitor other systems.

Navigate to:

```
Wazuh Dashboard → Agents → Deploy new agent
```

Choose your operating system:

* Linux
* Windows
* macOS

The dashboard will generate the installation command automatically.

Example Linux agent installation:

```bash id="k6n5t2"
curl -sO https://packages.wazuh.com/4.x/wazuh-agent.sh
sudo bash wazuh-agent.sh -a <MANAGER_IP>
```

---

# Useful Commands

| Command                           | Purpose             |
| --------------------------------- | ------------------- |
| `systemctl start wazuh-manager`   | Start Wazuh Manager |
| `systemctl stop wazuh-manager`    | Stop Manager        |
| `systemctl restart wazuh-manager` | Restart Manager     |
| `systemctl status wazuh-manager`  | Check status        |

---

# Official Wazuh Documentation

Official documentation:

https://documentation.wazuh.com

Installation guide:

https://documentation.wazuh.com/current/installation-guide/index.html

Wazuh GitHub:

https://github.com/wazuh/wazuh

---

# Author

Anurag Joseph

Cybersecurity Student

Gitam University

---

# Purpose of This Guide

This repository was created to help students and cybersecurity enthusiasts easily install **Wazuh SIEM** for security monitoring and SOC lab environments.

This setup can be used for:

* Security monitoring
* Log analysis
* Threat detection
* Vulnerability management
* SOC lab environments

---

# Next Steps

After installing Wazuh you can extend your SOC lab by integrating:

* Splunk SOAR (Phantom)
* Threat intelligence feeds
* Security automation playbooks

---

# License

This project is shared for educational purposes.
