# DevOps Quests 🚀

A collection of **real-world DevOps challenges** with step-by-step solutions.

## About
DevOps Quests is an open lab where:
- Anyone can propose challenges via GitHub Issues.
- Once accepted, a challenge can be implemented by anyone — including you.
- Solutions leverage modern tools (ArgoCD, Helm, Terraform, etc.) and run on Kubernetes as the infrastructure platform.
- Every solution should follow Infrastructure-as-Code principles as much as possible.
- Everyone is welcome to collaborate, learn, and improve together.

## Local Setup.

As long as you have Kubernetes and a default PVC storage class available, you can use this anywhere. If you’d like to set up a new development environment for testing, please follow this [guide](./docs/local_setup.md).

## Structure

- deployment/argocd: Installation of ArgoCD itself
- deployment/apps-inventory: Argo CD Applications Helm Chart. Basically a list of apps ArgoCD will deploy
- deployment/namespaces/`namespace`/`app`: Helm chart configuration for a given app in a given namespace
- docs/challenges: Basic overview of challenges
  - `challenges/01-tls-cert-automation`: Example solution for automatic TLS certificate management in Kubernetes using ArgoCD + Helm.

## How to Contribute
1. Check the [Issues](https://github.com/danielnegreiros/devops-quests/issues) for open challenges.
2. Suggest a new one using the [Challenge Template](.github/ISSUE_TEMPLATE/new-challenge.md).
3. Fork & PR your solution!
4. Contribute on opened issues

## 🔥 Challenges

> **[💡 TLS Certificates with Cloudflare, Cert-Manager & Kubernetes and supporting tools](./docs/challenges/01-tls-cert-automation/README.md)**  
Deploy a nearly 100% automated solution to issue & renew TLS certificates in a Kubernetes cluster with ArgoCD and Helm.


> **[🧭 Kube-bench Findings Scraper → DB → Visualization](./docs/challenges/02.kube-bench-exporter/README.md)**  
We need an application that collects kube-bench findings, stores them in a database, and makes them available for visualization in Grafana.
