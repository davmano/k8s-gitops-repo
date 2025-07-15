# 🚀 k8s-gitops-repo

> **Production-style GitOps repository** to deploy and manage a simple Flask application on Kubernetes,  
using **ArgoCD** for GitOps, **Prometheus & Grafana** for monitoring, and **Docker** + **GitHub Actions** for CI/CD.

---

## 📦 **Project structure**

```plaintext
k8s-gitops-repo/
├── apps/
│   └── flask-app/
│       ├── deployment.yaml         # Deployment for the Flask app
│       ├── service.yaml            # ClusterIP / LoadBalancer service
│       └── ingress.yaml            # Ingress resource
└── monitoring/
    ├── kube-prometheus-stack/
    │   └── values.yaml             # Custom values for Prometheus & Grafana
    └── prometheus-grafana-argocd.yaml   # ArgoCD Application resource to deploy monitoring

## 🌟 What this repo does

- ✅ Acts as the source of truth for your cluster
- ✅ ArgoCD continuously watches this repo:

    On every change, ArgoCD syncs the new manifests into Kubernetes
    ✅ Deploys:

    Flask app (Docker image: davmano/flask-aws_sm)

    Monitoring stack: Prometheus & Grafana (via Helm)

🚀 How it works (real-world GitOps flow)

1️⃣ Push code to your app repo → GitHub Actions:

    Builds & tags Docker image with commit SHA

    Scans with Trivy

    Pushes image to Docker Hub

    Clones this GitOps repo → updates deployment.yaml with new image tag → commits & pushes

2️⃣ ArgoCD sees new commit in this repo:

    Automatically applies changes to Kubernetes

    New version is deployed

3️⃣ Monitoring dashboards update automatically
📊 Monitoring (Prometheus & Grafana)

Installed via:

    monitoring/prometheus-grafana-argocd.yaml → ArgoCD deploys kube-prometheus-stack Helm chart

Grafana:

    Username: admin

    Password:

kubectl -n monitoring get secret kube-prometheus-stack-grafana \
  -o jsonpath="{.data.admin-password}" | base64 --decode

Access:

kubectl -n monitoring port-forward svc/kube-prometheus-stack-grafana 3000:80

Then open http://localhost:3000
⚙ Prerequisites

✅ Kubernetes cluster (e.g., Kind, Minikube, or EKS)
✅ ArgoCD installed in the cluster
✅ Docker Hub account
✅ GitHub Actions pipeline configured in app repo
📦 Deployment overview

    ArgoCD Application:

        monitoring/prometheus-grafana-argocd.yaml → deploys monitoring stack

    Flask app:

        apps/flask-app/deployment.yaml

        service.yaml

        ingress.yaml

📚 Technologies used

    Kubernetes

    ArgoCD

    GitHub Actions

    Docker

    Prometheus & Grafana

    Trivy (security scanning)

✏ Author

David Mano
LinkedIn
Docker Hub: davmano/flask-aws_sm
✅ License