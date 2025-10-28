# 👋 Hi! I'm Aleksandr Dobrynin

**DevOps/SRE Engineer** with 3+ years of experience building fault-tolerant infrastructure  
📍 Moscow | 🏠 Remote-friendly | 🇷🇺 Russian

---

## 🛠️ Technology Stack

**Infrastructure:** Linux (Debian/Ubuntu), Proxmox VE/PBS, Docker, KVM/LXC  
**Automation:** Bash, systemd, GitHub Actions, CI/CD  
**Databases:** PostgreSQL (replication, backups)  
**Networking:** nginx, VLAN, DNS, TLS (Let's Encrypt)  
**Monitoring:** Alarms, logging, capacity planning  

**Currently learning:** Kubernetes, Terraform, Ansible, Prometheus/Grafana

---

## 🚀 Projects

### [OAuth2 Infrastructure Automation](https://github.com/do6pbln9l/hh-oauth2-keendns-nginx-systemd)
OAuth2 infrastructure automation for HeadHunter API:
- ✅ CI/CD via GitHub Actions (ShellCheck, Docker build/push to GHCR)
- ✅ Automated token refresh via systemd timers (every 6 hours)
- ✅ nginx reverse-proxy + KeenDNS + Let's Encrypt
- ✅ Infrastructure as Code (all configs in Git)

**Technologies:** Docker, GitHub Actions, systemd, nginx, OAuth2

---

## 📊 Key Achievements

- ✅ **100% automation** of OAuth2 token refresh (was: manual every 2 weeks → now: systemd timer every 6 hours)
- ✅ **99.9% uptime** over the last 6 months (Proxmox VE HA cluster, 3 nodes)
- ✅ **RTO < 30 minutes** for service recovery (test-restores every 3 months)
- ✅ **CI/CD pipeline**: ShellCheck (100% compliance) + automated Docker builds to GHCR
- ✅ **Reduced toil from 40% to 10%** through automation of routine tasks

---

## 🏗️ Architecture

<details open>
  <summary>Click to collapse</summary>

![OAuth2 Infrastructure](https://github.com/do6pbln9l/hh-oauth2-keendns-nginx-systemd/blob/main/docs/images/oauth2-infrastructure-diagram.png?raw=true)

</details>

### 🖥️ View Mermaid diagram (desktop version)
<details close>
  <summary>Click to expand</summary>
  
```mermaid
flowchart TB
    subgraph infra["📦 OAuth2 Infrastructure (This repository)"]
        direction TB
        Nginx[🔄 nginx<br/>HTTP:80→:8000]
        
        subgraph automation["⚙️ Automation"]
            direction LR
            Timer[⏱️ systemd<br/>Every 6h]
            Script[📜 refresh.sh<br/>Token refresh]
        end
        
        TestServer[🧪 test-8000.py<br/>Test server]
        TokenStore[(🔐 Token Storage<br/>/var/lib/hh-token/token.json)]
    end
    
    subgraph prod["🤖 Production App (Separate project)"]
        direction TB
        TelegramBot[📱 Telegram Bot<br/>HH job search]
        FlaskApp[🌐 Flask Application<br/>OAuth callback handler at /callback]
        
        TelegramBot -.->|Project<br/>hh-oauth2-keendns-nginx-systemd| FlaskApp
    end
    
    subgraph external["External"]
        HHAPI[🏢 HH OAuth2 API<br/>api.hh.ru]
    end
    
    %% Connections / Component interactions
    
    %% Main Flow (OAuth):
    Nginx -->|1. Proxy :8000| FlaskApp
    FlaskApp -->|2. OAuth callback| HHAPI
    FlaskApp -->|3. Saves initial tokens| TokenStore
    
    %% Production Flow:
    FlaskApp -->|4. Reads tokens| TokenStore
    TelegramBot <-->|5. API requests| HHAPI
    
    %% Token Refresh Flow:
    Timer -.->|6. Trigger| Script
    Script -->|7. Refreshes tokens| HHAPI
    Script -->|8. Saves new tokens| TokenStore  
    
    %% Testing:
    TestServer -->|9. Testing alternative| Nginx
    
    %% Styling
    style Nginx fill:#2E8B57,color:#FFFFFF,stroke:#1a5f3a,stroke-width:2px
    style Timer fill:#FFA500,color:#000000,stroke:#cc8400,stroke-width:2px
    style Script fill:#FF8C00,color:#FFFFFF,stroke:#cc7000,stroke-width:2px
    style TestServer fill:#DAA520,color:#000000,stroke:#b8860b,stroke-width:2px
    style TokenStore fill:#9370DB,color:#FFFFFF,stroke:#6a4db8,stroke-width:2px
    
    style TelegramBot fill:#4682B4,color:#FFFFFF,stroke:#1565c0,stroke-width:2px
    style FlaskApp fill:#4169E1,color:#FFFFFF,stroke:#2a4ba8,stroke-width:2px
    
    style HHAPI fill:#DC143C,color:#FFFFFF,stroke:#a00000,stroke-width:2px

```
  
### Color Legend

- 🟢 Green — infrastructure components (nginx)
- 🟠 Orange — automation (systemd timer, Bash scripts)
- 🟡 Gold — testing/auxiliary tools (test-8000.py)
- 🟣 Purple — data storage (Token Storage)
- 🔵 Blue — production application (Telegram Bot, Flask App)
- 🔴 Red — external APIs (HeadHunter)

</details>

---

## 📫 Contact

💼 HH.ru: [DevOps/SRE Resume](https://hh.ru/resume/e2cf5fedff07cc20d30039ed1f494e42465951?from=share_ios)

💬 **Preferred contact method:** Apply via HH or email from resume 

---

🏠 **Working from home** | 🌟 **Open to DevOps/SRE opportunities**

