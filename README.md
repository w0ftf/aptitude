# Automation, DevOps, IaC

This repository is my hands-on automation workspace. 

## Core Skill Areas

- Linux automation with Bash for system setup, maintenance, and reporting
- AWS operations automation (CloudWatch, EC2, SSM, and CLI-driven workflows)
- Infrastructure as Code with Ansible playbooks/roles and Terraform
- Monitoring and observability automation (CloudWatch agents/alarms, SignalFx workflows)
- API scripting for admin tasks (for example, account/user lifecycle actions)
- AI agent and bot tasks automation (OpenAI, Claude, DeepSeek, Ollama, Hugging Face)
- Legacy bot/chat automation with Tcl and Perl scripting
- Multi-agent orchestration with shared-database task queues (PostgreSQL row locking/claiming, staged synthesis of multiple model outputs into one answer)
- Agentic tool-use loops (Claude/LLM-driven sequencing of external API calls, ReAct-style agents with sandboxed file/shell tool access)
- Full-stack AI web app deployment (Flask APIs behind Apache/systemd or Docker + supervisord, with CI/CD via GitHub Actions self-hosted runners)
- Containerized database provisioning and tuning (Dockerized PostgreSQL, pg_hba.conf access control, performance/logging configuration)
- Kubernetes/k3s deployment for load-balanced, self-healing web apps (Traefik ingress, WebSocket bridging, health probes)

## Representative Works

### AI
- AI backend or persona such as OpenAI, Claude, DeepSeek, Ollama, Hugging Face, or a pentesting-focused setup, while offering broadly similar chat and automation behavior
- Features like channel replies, logging, conversation memory, search or utility commands, and per-channel AI on/off controls, with settings loaded from local config files

### AI Bot & Multi-Agent Systems (IRC/Sopel)
- A shared IRC (Sopel) plugin architecture with ~10 interchangeable model backends (OpenAI, Claude, DeepSeek, Ollama, Hugging Face) exposing near-identical utility commands (search, weather, port checks, quote/log search, per-channel AI toggles)
- A multi-agent panel orchestrator (`control_tower.py`) that fans a question out to a small set of bots, runs one shared web-research pass, and synthesizes the replies into a single consolidated answer
- A shared PostgreSQL coordination layer (`ai_coordination.py`) implementing round/task/result tables, atomic task claiming with `FOR UPDATE SKIP LOCKED`, staged rebuttal rounds, and graceful degradation when a worker or search call fails
- Full-text + fallback keyword search (`to_tsvector`/`to_tsquery` with `ILIKE` fallback) over historical bot conversation logs, synthesized into concise answers by a local Ollama model at zero API cost
- A security/pentest-focused assistant bot with an allowlisted command-execution mode (nmap, nikto, sqlmap, etc.) and a separate ReAct-style autonomous agent mode (path-restricted file read/write/delete, restricted shell commands, iteration caps)
- Shared helper modules for cross-cutting bot features: PrivateBin paste review/apply (fetch, decrypt, edit, re-upload), join-notice + RSS news polling, and channel logging/search
- Deployment/packaging quirks for pipx-installed Sopel (copying shared modules into the isolated venv's site-packages so plugins can import them)

### AI Web Applications & Agentic Tools
- Agentic tool-use loops where an LLM (Claude) sequences external API calls with error recovery — e.g., a natural-language Okta user/group management agent (create user → find group → add to group, with lookup fallback on conflict)
- Full-stack deployment patterns for these agents: Apache reverse-proxying to a Flask/systemd backend, or a Docker image managed by supervisord (Apache + Flask) with GitHub Actions self-hosted-runner CI/CD (build, replace container, health-check on every push to main)
- CLI and web-UI parity for the same agent backend (interactive/one-shot CLI script alongside the HTTP API)
- Static single-file site deployment (no build step, no external assets) as a lightweight alternative when a full app isn't warranted

### Containers, Databases & Kubernetes
- Dockerized PostgreSQL provisioning with custom images, host/unix-socket access control via `pg_hba.conf`, and tuning of memory/WAL/query-planning/logging settings in `postgresql.conf`
- k3s (lightweight Kubernetes) deployment of a load-balanced, self-healing web app: Traefik ingress, multi-replica Deployment, ClusterIP service, liveness/readiness health probes, and a WebSocket-to-external-service bridge running per pod
- Scripted install/build/deploy/teardown workflows (`deploy.sh`/`teardown.sh`) so a k3s demo environment can be stood up and torn down repeatably

### Shell Automation

- CloudWatch alarm provisioning and metric automation
- Remote CloudWatch Agent deployment and configuration
- SSM agent install automation across Linux distributions
- Splunk forwarder deployment and service bootstrap scripts
- Domain MX audit/export tooling for operations reporting
- Debian update + email reporting workflow

### Ansible Automation

- EC2 instance provisioning role 
- Demisto, SOAR, SIEM deployment/upgrade automation
- System update orchestration
- Host-level operational playbooks

### Terraform IaC

- AWS instance build configurations
- Snapshot and environment infrastructure workflows
- SignalFx detector and alert definitions
- Reusable module patterns

### Additional Scripting

- API cleanup scripts
- Python utilities
- IRC/bot ecosystem scripting

## Tooling I Work With

- Bash, Python, Tcl, Perl
- Ansible
- Terraform
- AWS CLI
- Linux service/process tooling (systemd, package managers, SSH/SCP)
- Splunk Forwarder and CloudWatch Agent operations
- Docker, Docker Compose, and Kubernetes (k3s), including supervisord multi-process containers
- PostgreSQL (schema design, full-text search, row-locking task queues, access/config tuning)
- Sopel IRC bot framework, Flask, Apache/systemd, GitHub Actions (self-hosted runners)
- LLM/agent APIs and tool-use loops: Anthropic Claude, OpenAI, DeepSeek, Ollama, Hugging Face

## Focus

My strongest area is practical operations automation: turning recurring infrastructure and support tasks into repeatable scripts and infrastructure definitions.