# Docker Compose Quick Start Guide

## Prerequisites
- Docker installed
- Docker Compose installed

## Quick Start Commands

```bash
# 1. Clone the repository
git clone <your-repo-url>

# 2. Navigate to project directory
cd <your-repo-name>

# 3. Start the entire stack (web servers + monitoring)
docker compose -f docker-compose.metrics.yaml up -d

# 4. Verify all containers are running
docker ps

# 5. Access the services
```

## Service URLs

| Service | URL | Description |
|---------|-----|-------------|
| **Main Website** | http://localhost | NGINX load balancer (cycles through web1, web2, web3) |
| **Grafana Dashboard** | http://localhost:3000 | Login: `admin` / `admin` |
| **Prometheus** | http://localhost:9090 | Metrics database |
| **NGINX Metrics** | http://localhost:9113/metrics | Raw NGINX metrics |
| **System Metrics** | http://localhost:9100/metrics | Host system metrics |

## Setup Grafana (First Time)

```bash
# 6. Open Grafana at http://localhost:3000
# 7. Login with admin/admin (change password when prompted)
# 8. Add Prometheus data source:
#    - Go to Configuration → Data Sources
#    - Add Prometheus
#    - URL: http://prometheus:9090
#    - Save & Test
# 9. Import dashboard ID: 12708 for NGINX monitoring
```

## Generate Test Traffic

```bash
# 10. Simulate traffic to see metrics in action
for i in {1..100}; do curl http://localhost; sleep 1; done
```

## Stop the Stack

```bash
# 11. Stop all services
docker compose -f docker-compose.metrics.yaml down
```

## Troubleshooting

```bash
# View logs for specific service
docker logs <container-name>

# View all container logs
docker compose -f docker-compose.metrics.yaml logs

# Restart specific service
docker compose -f docker-compose.metrics.yaml restart <service-name>
```

That's it! Your multi-container web stack with full observability is now running.