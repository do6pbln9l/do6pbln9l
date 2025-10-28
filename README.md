# 👋 Привет! Я Александр Добрынин

**DevOps/SRE-инженер** с 3+ годами опыта построения отказоустойчивой инфраструктуры  
📍 Москва | 🏠 Remote-friendly | 🇷🇺 Русский

---

## 🛠️ Технологический стек

**Инфраструктура:** Linux (Debian/Ubuntu), Proxmox VE/PBS, Docker, KVM/LXC  
**Автоматизация:** Bash, systemd, GitHub Actions, CI/CD  
**Базы данных:** PostgreSQL (репликация, backups)  
**Сети:** nginx, VLAN, DNS, TLS (Let's Encrypt)  
**Мониторинг:** Alarms, logging, capacity planning  

**В изучении:** Kubernetes, Terraform, Ansible, Prometheus/Grafana

---

## 🚀 Проекты

### [OAuth2 Infrastructure Automation](https://github.com/do6pbln9l/hh-oauth2-keendns-nginx-systemd)
Автоматизация OAuth2-инфраструктуры для HeadHunter API:
- ✅ CI/CD через GitHub Actions (ShellCheck, Docker build/push в GHCR)
- ✅ Автообновление токенов через systemd timers (каждые 6 часов)
- ✅ nginx reverse-proxy + KeenDNS + Let's Encrypt
- ✅ Infrastructure as Code (все конфигурации в Git)

**Технологии:** Docker, GitHub Actions, systemd, nginx, OAuth2

---

## 📊 Ключевые достижения

- ✅ **100% автоматизация** обновления OAuth2 токенов (было: вручную каждые 2 недели → стало: systemd timer каждые 6 часов)
- ✅ **Uptime 99.9%** за последние 6 месяцев (Proxmox VE HA-кластер, 3 ноды)
- ✅ **RTO < 30 минут** для восстановления сервисов (test-restores каждые 3 месяца)
- ✅ **CI/CD pipeline**: ShellCheck (100% compliance) + Docker автосборка в GHCR
- ✅ **Сокращение toil с 40% до 10%** через автоматизацию рутинных задач

---

## 🏗️ Архитектура

<details open>
  <summary> Click to collapse</summary>

![OAuth2 Infrastructure](https://github.com/do6pbln9l/hh-oauth2-keendns-nginx-systemd/blob/main/docs/images/oauth2-infrastructure-diagram.png?raw=true)

</details>

### 🖥️ View Mermaid diagram (desktop version)
<details close>
  <summary> Click to expand</summary>

```mermaid
flowchart TB
    
    subgraph infra["📦 OAuth2 Infrastructure (Этот репозиторий)"]
        direction TB
        Nginx[🔄 nginx<br/>HTTP:80→:8000]
        
        subgraph automation["⚙️ Automation"]
            direction LR
            Timer[⏱️ systemd<br/>Каждые 6h]
            Script[📜 refresh.sh<br/>Обновление токенов]
        end
        
        TestServer[🧪 test-8000.py<br/>Тестовый сервер]
        TokenStore[(🔐 Token Storage<br/>/var/lib/hh-token/token.json)]
    end
    
    subgraph prod["🤖 Production App (Отдельный проект)"]
        direction TB
        TelegramBot[📱 Telegram Bot<br/>Поиск вакансий HH]
        FlaskApp[🌐 Flask Application<br/>Обработка OAuth callback на /callback]
        
        TelegramBot -.->|Проект<br/>hh-oauth2-keendns-nginx-systemd| FlaskApp
    end
    
    subgraph external["External"]
        HHAPI[🏢 HH OAuth2 API<br/>api.hh.ru]
    end
    
    %% Connections / Связи между компонентами

    %% Main Flow (OAuth) (основной поток):
    Nginx -->|1. Proxy :8000| FlaskApp
    FlaskApp -->|2. OAuth callback| HHAPI
    FlaskApp -->|3. Сохраняет первый tokens| TokenStore

    %% Production Flow (работа приложения):
    FlaskApp -->|4. Считывание tokens| TokenStore
    TelegramBot <-->|5. API запросы| HHAPI

    %% Token Refresh Flow (автоматизация):
    Timer -.->|6. Trigger| Script
    Script -->|7. Обновляет tokens| HHAPI
    Script -->|8. Сохраняет new tokens| TokenStore  

    %% Testing (тестирование):
    TestServer -->|9. Альтернатива для<br/>тестирования| Nginx
    
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

### Цветовая схема

- 🟢 Зелёный — инфраструктурные компоненты (nginx)
- 🟠 Оранжевый — автоматизация (systemd timer, Bash scripts)
- 🟡 Золотой — тестовые/вспомогательные инструменты (test-8000.py)
- 🟣 Фиолетовый — хранилище данных (Token Storage)
- 🔵 Синий — продакшен-приложение (Telegram Bot, Flask App)
- 🔴 Красный — внешние API (HeadHunter)

</details>

---

## 📫 Контакты

💼 HH.ru: [Резюме DevOps/SRE](https://hh.ru/resume/e2cf5fedff07cc20d30039ed1f494e42465951?from=share_ios)

💬 **Предпочитаемый способ связи:** Отклик через HH или email из резюме 

---

🏠 **Working from home** | 🌟 **Open to DevOps/SRE opportunities**
