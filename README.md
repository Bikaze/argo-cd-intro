# ArgoCD Demo

Simple ArgoCD GitOps demo following [TechWorld with Nana's YouTube course](https://www.youtube.com/watch?v=MeU5_k9ssrs).

## Prerequisites

- Kubernetes cluster (local or cloud)
- kubectl configured and connected to your cluster
- Git repository access

## Project Structure

```text
├── application.yaml      # ArgoCD Application configuration
└── dev/
    ├── deployment.yaml   # Kubernetes Deployment
    └── service.yaml      # Kubernetes Service
```

## Setup ArgoCD

1. **Create namespace:**

   ```bash
   kubectl create namespace argocd
   ```

2. **Install ArgoCD:**

   ```bash
   kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
   ```

3. **Access ArgoCD UI:**

   ```bash
   kubectl port-forward svc/argocd-server -n argocd 8080:443
   ```

4. **Get admin password:**

   ```bash
   kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
   ```

## Deploy Application

Apply the ArgoCD application:

```bash
kubectl apply -f application.yaml
```

## Application Details

- **Image:** `nanajanashia/argocd-app:1.2`
- **Replicas:** 2
- **Port:** 8080
- **Namespace:** myapp (auto-created)
- **Sync Policy:** Automated with prune and self-heal

## More Information

[ArgoCD Getting Started Guide](https://argo-cd.readthedocs.io/en/stable/getting_started/)
