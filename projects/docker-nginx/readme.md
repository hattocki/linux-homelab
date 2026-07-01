# Docker Nginx Service

## Architecture

```
        Windows (Git + VS Code)
                 |
                 |
        ----------------------
        |                    |
   VM1 (Server)         VM2 (Monitoring - future)
        |
        |
   Docker + Nginx
        |
        |
   Port 8080 exposed
```

---

## Goal

Deploy a web server (Nginx) using Docker on Ubuntu VM and expose it via network.

---

## System Design

- VM1 acts as a production-like server
- Docker is used for containerization
- Nginx runs as a containerized web service
- Port 8080 is exposed to the host machine
- VM2 will be used later for monitoring (Prometheus/Grafana stack)

---

## Real-world relevance

This setup simulates a basic production environment where:
- applications run in containers
- services are isolated using Docker
- network ports are explicitly exposed
- monitoring is separated into a dedicated node

---

## Environment

- Ubuntu Server (VM1)
- Docker Engine
- Nginx container
- Windows host machine (Git + VS Code)

---

## Steps performed

1. Updated system packages
2. Installed Docker
3. Started and enabled Docker service
4. Verified Docker installation
5. Ran test container (hello-world)
6. Deployed Nginx container with port mapping

---

## Result

Nginx web server is running inside a Docker container and is accessible via:

```
http://VM1-IP:8080
```

---

## Notes

VM2 is reserved for future monitoring setup (Prometheus, Grafana, system metrics).