# DevOps Starter: CI/CD, Dockerized Deployment & Monitoring on AWS

## Overview

Deploy a fullstack application (React frontend and Node.js backend) using containerization, CI/CD pipelines, and monitoring tools. The deployment must be performed on AWS EC2 using the AWS free tier. You will take your existing applications (A Node.js backend and React frontend) and:

* Build a CI/CD pipeline using GitHub Actions
* Containerize the applications using Docker
* Deploy the containers on AWS EC2 (free tier)
* Set up basic monitoring using Prometheus and Grafana or AWS CloudWatch
* Perform load testing and integrate user acceptance test (UAT) stages

---

## Prerequisites

* GitHub account
* AWS free-tier account (create at [aws.amazon.com](https://aws.amazon.com), check free tier limits; reversible card transaction may occur)
* React and Node.js projects (you can use your own or clone open-source projects)

---

## Step-by-Step Tasks

### 1. CI/CD Pipeline with GitHub Actions

* Set up GitHub Actions to automate the following:

  * Install dependencies
  * Run test cases (use **Jest** for Node, **Cypress** or **React Testing Library** for frontend)
  * Build Docker images using local `Dockerfile`
  * SSH into the EC2 instance and deploy the app using `docker run` or `docker-compose`

* Keep separate workflows for backend and frontend, or combine them based on your repo layout.

### 2. Containerization with Docker

* Create a `Dockerfile` for both React and Node.js applications.
* React app should use `npm run build` and serve the static files via **Nginx** inside the container.
* Node.js app can be served directly via `node` or better using **PM2** for process management.
* Optionally, use `docker-compose` for running both services together in development or on the EC2 instance.

### 3. AWS EC2 Deployment (Free Tier)

* Launch an EC2 instance (Ubuntu 22.04 or Amazon Linux 2 preferred).
* SSH into the EC2 instance, install Docker and Docker Compose.
* Transfer your built Docker images or `docker-compose.yml` to the server (or build them directly on EC2).
* Run your containers:

  * React container on port `80` (Nginx)
  * Node.js API container on port `3000` or any custom API port
* Set up a security group to allow inbound traffic (HTTP, HTTPS, SSH).

### 4. Monitoring and Logging

* **Option 1: Prometheus + Grafana**

  * Run Prometheus and Grafana as Docker containers on the same EC2 instance.
  * Configure Prometheus to scrape metrics from Node.js and Docker if available.
  * Set up Grafana dashboards to monitor application health and server metrics.

* **Option 2: AWS CloudWatch**

  * Install and configure CloudWatch agent on EC2.
  * Push logs and basic metrics (CPU, memory, disk) to AWS CloudWatch.
  * Set alerts/alarms as needed.

### 5. UAT and Load Testing

* Create a GitHub Actions job that runs user acceptance tests automatically after each deployment.
* Use tools like `k6` or `Apache JMeter` to simulate realistic traffic and test backend/API performance.
* Optionally, schedule these tests periodically using GitHub Actions workflow triggers or cron.

---

## Summary of Tools Used

| Tool           | Purpose                           |
| -------------- | --------------------------------- |
| GitHub Actions | CI/CD automation                  |
| Docker         | Containerization                  |
| AWS EC2        | Application hosting               |
| Nginx          | Static file server for React app  |
| PM2            | Node.js process management        |
| Prometheus     | Metrics collection (optional)     |
| Grafana        | Metrics dashboard (optional)      |
| AWS CloudWatch | Logging and monitoring (optional) |
| k6/JMeter      | Load and performance testing      |
| Jest/Cypress   | Test automation                   |

---

## Final Notes

* Make sure to shut down or clean up AWS resources after testing to avoid unexpected charges.
* Monitor AWS usage regularly if you're on the free tier.
* You can extend this project to include a domain name, HTTPS setup (via AWS ACM), and autoscaling using ECS later.

