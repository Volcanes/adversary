# Prerequisites

## 1. Overview

This document describes the hardware, software and network requirements
needed to deploy the cybersecurity lab.

The lab consists of the following components:

- **Elasticsearch:** Stores, indexes and searches security data.
- **Kibana:** Provides the web interface for data visualization and analysis.
- **Fleet Server:** Manages Elastic Agents and their policies.
- **Caldera:** Provides adversary emulation capabilities through operations
  and agents.
- **Elastic Agents:** Collect and send telemetry from monitored systems.

Elasticsearch and Kibana run in Docker containers. Fleet Server and Caldera
are installed directly on the host operating system.

## 2. Hardware Requirements

The following are suggested starting points for a small home lab.
Actual requirements depend on the number of agents, the volume of telemetry
and the duration of data retention.

| Resource | Minimum starting point | Recommended |
|---|---|---|
| CPU | 4 cores | 8 cores |
| RAM | 8 GB | 16–32 GB |
| Storage | 50 GB free | 100 GB or more |
| Network | Ethernet or Wi-Fi | Stable wired connection |

> These values are estimates for a small lab, not official minimum
> requirements for every component. Elasticsearch, Caldera and the agents
> may require additional resources depending on the workload.

## 3. Operating System

The host machine should run a supported Linux distribution. 

The lab has been designed around an Ubuntu 26.04 environment.

You should have:

- A working Linux installation.
- A user account with `sudo` privileges.
- Internet access to download packages and container images.
- Network connectivity between the lab components.

If you are running Ubuntu inside a virtual machine, ensure that the VM has
sufficient CPU, RAM and disk space allocated.

## 4. Required Software

Install or prepare the following components before proceeding.

### 4.1. Docker

Docker is used to run Elasticsearch and Kibana.

Verify the installation:

```bash
docker --version
docker compose version
```

Check that Docker is running:

```bash
docker ps
```

If these commands fail, complete the Docker installation and configuration
before continuing.

### 4.2. Git

Git is required to download the lab repository.

Verify the installation:

```bash
git --version
```

If Git is not installed, install it with:

```bash
sudo apt update
sudo apt install git
```

### 4.3. Python

Python is required for the host-based Caldera installation.

Check the installed version:

```bash
python3 --version
pip3 --version
```

The Python version must be compatible with the Caldera version used in
this lab.


## 5. Network and Ports

The following ports may be used by the lab.

| Component | Port | Purpose |
|---|---:|---|
| Elasticsearch | 9200 | Elasticsearch HTTP API |
| Kibana | 5601 | Web interface |
| Fleet Server | 8220 | Elastic Agent communication |
| Caldera | 8888 | Web interface, depending on configuration |

These are the expected default ports. Verify the actual port mappings and
listener configuration before starting the lab.

Check whether a port is already in use:

```bash
sudo ss -lntp
```

If you are using a virtual machine, configure networking so that the systems
and agents can reach the services they need.

Do not expose Elasticsearch, Kibana, Fleet Server or Caldera directly to
the public Internet.

## 6. Credentials and Configuration

Before starting the lab:

- Prepare the required environment variables in the `.env` file.
- Use strong, unique passwords.
- Keep real credentials out of GitHub.
- Do not commit the `.env` file to the repository.
- Use `.env.example` as a template, REPLACE THE KEYS. 

The installation guide explains how to configure these variables.

## 7. Installation Order

The lab should be prepared in the following order:

1. Install and verify Docker and Docker Compose.
2. Download the lab repository.
3. Configure the `.env` file.
4. Start Elasticsearch and Kibana.
5. Verify that Elasticsearch and Kibana are accessible.
6. Install and configure Fleet Server on the host.
7. Install and configure Caldera on the host.
8. Deploy and configure the agents required for the exercises.
9. Verify connectivity between the components.

Follow the installation guides for the exact commands and configuration
details.

## 8. Security Considerations

This environment is intended for educational and controlled testing purposes.

- Run Caldera operations only against systems you own or are explicitly
  authorized to test.
- Do not expose management interfaces to untrusted networks.
- Protect passwords, API keys and certificates.
- Use appropriate TLS certificates and authentication.
- Review firewall rules and exposed ports before running the lab.

## 9. Next Steps

Once all prerequisites are satisfied, continue with the installation guide:

[Elasticsearch Installation](02-installation-elasticsearch.md)
