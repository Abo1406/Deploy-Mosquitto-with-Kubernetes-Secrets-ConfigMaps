# Mosquitto MQTT Broker Deployment with Kubernetes Secrets and ConfigMaps

![Kubernetes](https://img.shields.io/badge/kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)
![Mosquitto](https://img.shields.io/badge/Mosquitto-3C5280?style=for-the-badge&logo=eclipsemosquitto&logoColor=white)

This project demonstrates secure deployment of an Eclipse Mosquitto MQTT message broker on Kubernetes using ConfigMaps for configuration management and Secrets for sensitive data handling.

## Features
- 🔒 Secure password storage using Kubernetes Secrets
- ⚙️ Centralized configuration management via ConfigMaps
- 🔁 Multi-replica deployment for high availability
- 📝 Structured logging with timestamps
- 🔐 Read-only secret volume mounts

## Prerequisites
- Kubernetes cluster (v1.18+)
- `kubectl` configured to access your cluster
- Basic understanding of Kubernetes concepts

## Project Structure
Deploy-Mosquitto-with-Kubernetes-Secrets-ConfigMaps/

├── config-file.yml # Mosquitto configuration ConfigMap

├── secret-file.yml # Password Secret definition

└── mosquitto.yml # Deployment manifest

## Deployment Instructions

### 1. Create the ConfigMap
```bash
kubectl apply -f config-file.yml
```
### 2. Create the Secret
```bash
kubectl apply -f secret-file.yml
```
### 3. Deploy Mosquitto
```bash
kubectl apply -f mosquitto.yml
```
### 4. Verify deployment
```bash
kubectl get all -l app=mosquitto
```
```bash
Expected output:
NAME                             READY   STATUS    RESTARTS   AGE
pod/mosquitto-7ddc67b6cd-fphcb   1/1     Running   0          5m
pod/mosquitto-7ddc67b6cd-jwl74   1/1     Running   0          5m

NAME                        READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/mosquitto   2/2     2            2           5m

NAME                                   DESIRED   CURRENT   READY   AGE
replicaset.apps/mosquitto-7ddc67b6cd   2         2         2       5m
```
### Configuration Details
ConfigMap (config-file.yml)

Mounts to: /mosquitto/config

Configuration parameters:
```bash
log_dest stdout     # Output logs to standard output
log_type all        # Log all message types
log_timestamp true  # Include timestamps in logs
listener 9001       # Listen on port 9001
```
