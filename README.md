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

