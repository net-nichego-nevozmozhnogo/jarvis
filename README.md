# n8n Self-Hosted Infrastructure

Automated, self-hosted deployment of **n8n** using **Docker Compose**, **Traefik** (reverse proxy with automated Let's Encrypt SSL), **PostgreSQL**, **Ansible**, and **GitHub Actions** for Continuous Deployment (CD).

## Tech Stack

- **Workflow Automation:** [n8n](https://n8n.io/)
- **Database:** PostgreSQL 16
- **Reverse Proxy & SSL:** Traefik v3 (TLS via Let's Encrypt)
- **Configuration Management:** Ansible
- **CI/CD:** GitHub Actions

## Repository Structure

```text
.
├── .github/
│   └── workflows/
│       └── deploy.yml       # GitHub Actions CD pipeline
├── ansible/
│   ├── inventory.ini        # Ansible target server inventory
│   └── setup-server.yml     # Server provisioning playbook
├── n8n/
│   ├── docker-compose.yml   # Container stack specification
│   └── .env.example         # Environment variables template
└── README.md

```

## Setup Instructions

### 1. Configure GitHub Secrets

Navigate to **Settings > Secrets and variables > Actions** in your GitHub repository and add the following repository secrets:

| Secret Name | Description | Example |
| --- | --- | --- |
| `SERVER_IP` | Remote server IP address | `123.45.67.89` |
| `SERVER_PASSWORD` | SSH root password | `your_server_password` |
| `N8N_HOSTNAME` | Domain or sslip.io host | `n8n.123.45.67.89.sslip.io` |
| `SSL_EMAIL` | Email for Let's Encrypt SSL certificates | `admin@example.com` |
| `POSTGRES_USER` | PostgreSQL username | `n8n_user` |
| `POSTGRES_PASSWORD` | PostgreSQL password | `strong_db_password` |
| `POSTGRES_DB` | PostgreSQL database name | `n8n_db` |
| `GENERIC_TIMEZONE` | Timezone for n8n triggers | `Europe/Kyiv` |
| `N8N_ENCRYPTION_KEY` | Secret key (32+ chars) for encryption | `a8f9c1e2d3b4567890abcdef12345678` |

### 2. Deploy via CI/CD

Push your code to the `main` branch to trigger the automated deployment:

```bash
git add .
git commit -m "feat: initial infrastructure setup"
git push origin main

```

Alternatively, run the workflow manually from the **Actions** tab in GitHub.

### 3. Access n8n

After the workflow completes (approx. 2–3 minutes):

1. Open `https://<N8N_HOSTNAME>` in your browser.
2. Complete the initial owner account registration.