# Multibranch Pipeline with Jenkins & Docker

![Jenkins](https://img.shields.io/badge/jenkins-%232C5263.svg?style=for-the-badge&logo=jenkins&logoColor=white)
![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)
![NodeJS](https://img.shields.io/badge/node.js-6DA55F?style=for-the-badge&logo=node.js&logoColor=white)
![GitHub](https://img.shields.io/badge/github-%23121011.svg?style=for-the-badge&logo=github&logoColor=white)
![Groovy](https://img.shields.io/badge/Groovy-4298B8?style=for-the-badge&logo=Apache+Groovy&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)

## Project Overview
This repository contains the final laboratory project for the **EPAM Cloud & DevOps Nextgen Internship**. The goal of this project is to implement a robust Continuous Integration and Continuous Deployment (CI/CD) workflow using a **Jenkins Multibranch Pipeline**. 

The pipeline automatically detects branches in the GitHub repository, builds a Node.js application, tests it, creates a Docker image, and deploys it in isolated environments based on the branch name.

## Architecture & Branching Strategy
To simulate different deployment environments (Production and Development) on a single host, the declarative `Jenkinsfile` uses conditional logic to assign specific ports, image names, and container names based on the active branch:

| Environment | Branch | Docker Image | Port | Container Name | Visual Indicator |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Production** | `main` | `nodemain:v1.0` | `3000` | `app_main` | Original Logo |
| **Development**| `dev` | `nodedev:v1.0` | `3001` | `app_dev` | Custom Logo |

## Pipeline Stages
The `Jenkinsfile` is written in Groovy and executes the following automated stages:
1. **Checkout SCM:** Pulls the latest source code from the triggered GitHub branch.
2. **Build:** Uses Node.js (v7.8.0) to install application dependencies (`npm install`).
3. **Test:** Runs the automated testing suite (`npm test`).
4. **Build Docker Image:** Containerizes the application using the dynamically assigned image name.
5. **Deploy:** Stops/removes any existing container for that branch and deploys the new container on the designated port.

## Technologies Used
* **Jenkins:** CI/CD Automation Server.
* **Docker:** Containerization engine.
* **Node.js (v7.8.0):** Application runtime environment.
* **Git & GitHub:** Version control and source code management.
* **Groovy:** Scripting language used for the declarative Jenkinsfile.

## How it works
1. A developer pushes code to either the `main` or `dev` branch.
2. Jenkins detects the change via periodic repository scanning (or webhooks).
3. The Multibranch Pipeline reads the `Jenkinsfile` and executes the build process.
4. The application is instantly available on `localhost:3000` (Production) or `localhost:3001` (Development) without manual intervention.

# Thank you EPAM for all this amazing learning experience!!
---
*Created as part of the EPAM DevOps Nextgen program.*
