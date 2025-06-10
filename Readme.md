<p align="center">
  <img src="assets/images/Linux-docker-orbit.png" alt="Linux Docker Orbit" />
</p>

# 🐳 Apache + NGINX + Observability with Docker Compose on Linux Mint

Welcome! This project is a hands-on guide where I set up a **simple load-balanced web server environment using Docker**, and then layered on **observability tools** like Prometheus and Grafana to monitor everything. The goal was to learn how multiple containers can work together — and how to see what they're doing under the hood.

---

## 🧭 Project Overview

- I customized **three Apache web servers** (`web1`, `web2`, `web3`) each serving a slightly different static page.
- I placed an **NGINX reverse proxy** in front to load balance traffic across them.
- Then I added **metrics & dashboards** using Docker Compose to monitor requests, CPU, and more.
- Everything runs with just a few Docker Compose commands.

---

## 📁 What This Project Includes

### [⚙️ Phase 1: Basic Docker Commands](#)
A quick reference of all the Docker CLI commands I used (run, stop, exec, remove, etc.).

### [🔁 Phase 2: Multiple Apache Containers](#)
I ran 3 separate Apache containers and customized their `index.html` pages to identify each one.

### [🌐 Phase 3: Load Balancing with NGINX](#)
I added an `nginx.conf` to reverse proxy all three Apache servers using **round-robin load balancing**.

### [📊 Phase 4: Observability with Prometheus & Grafana](#)
I used a second Compose file to add:
- `nginx-exporter`, `node-exporter` (for metrics)
- `prometheus.yaml` (for scrape config)
- `status.conf` (to expose Apache metrics)
- Grafana dashboards

---

## 🎯 Why I Built This

I wanted to understand how real-world web services are structured:
- How traffic gets distributed between servers.
- How you can observe performance in real time.
- How Docker Compose simplifies multi-service orchestration.

This project gave me a full-stack understanding of container networking, monitoring, and service design — all using open-source tools.

---

## 🏁 Quick Start

1. Clone this repo  
2. Start the basic services:  
   `'docker compose up -d'`
3. Add observability:  
   `'docker compose -f docker-compose.yaml -f docker-compose.metrics.yaml up -d'`
4. Open your browser:
   - Web: http://localhost:8080  
   - Prometheus: http://localhost:9090  
   - Grafana: http://localhost:3000 (`admin/admin`)

---

## 📎 File Structure
``` 
project-file-structure/
├── docker-compose.yaml # Apache + NGINX
├── docker-compose.metrics.yaml # Metrics stack
├── nginx.conf # Load balancing config
├── prometheus.yaml # Prometheus scrape config
├── status.conf # Apache status module
├── index1.html / index2.html / index3.html
``
---

## 🙌 Built With

- Docker & Docker Compose
- Apache HTTPD (web server)
- NGINX (reverse proxy)
- Prometheus (metrics)
- Grafana (dashboards)

## Future Development - 
I'll be experimenting with other metric collection methods (httpd metrics) 
and a few automation modalitits in the future, so be sure to check back in from time to time!

Enjoy!