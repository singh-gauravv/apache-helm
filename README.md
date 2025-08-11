# apache-helm

A Helm chart for deploying an Apache HTTP server on Kubernetes.  
This chart includes configuration for Deployment, Service, Ingress, ServiceAccount, and HorizontalPodAutoscaler,  
with flexible customization through `values.yaml`.

---

## 📂 Project Structure

```
apache-helm/
  Chart.yaml          # Chart metadata
  values.yaml         # Default configuration values
  templates/          # Kubernetes manifests with Helm templating
    deployment.yaml
    service.yaml
    ingress.yaml
    hpa.yaml
    serviceaccount.yaml
    _helpers.tpl
    NOTES.txt
```

---

## 🚀 Prerequisites

- [Helm 3+](https://helm.sh/docs/intro/install/)
- A running Kubernetes cluster (Minikube, Kind, GKE, EKS, AKS, etc.)
- `kubectl` configured to talk to your cluster

---

## 📦 Installation

1. **Clone this repository**:
   ```bash
   git clone https://github.com/<your-username>/apache-helm.git
   cd apache-helm
   ```

2. **Install the chart**:
   ```bash
   helm install my-apache ./apache-helm
   ```

3. **Verify deployment**:
   ```bash
   kubectl get pods
   kubectl get svc
   ```

---

## ⚙️ Configuration

All configurable values are in [`values.yaml`](./values.yaml).  
You can override any value using the `--set` flag or by providing your own `my-values.yaml`.

Example:
```bash
helm install my-apache ./apache-helm --values my-values.yaml
```

### Common Parameters

| Parameter | Description | Default |
|-----------|-------------|---------|
| `replicaCount` | Number of pod replicas | `3` |
| `image.repository` | Container image repository | `httpd` |
| `image.tag` | Container image tag | `2.4` |
| `service.type` | Kubernetes service type | `ClusterIP` |
| `service.port` | Service port | `80` |
| `ingress.enabled` | Enable ingress controller | `false` |
| `autoscaling.enabled` | Enable HPA | `false` |

---

## 🌐 Accessing the Application

- **Without Ingress** (NodePort):
  ```bash
  export NODE_PORT=$(kubectl get --namespace default -o jsonpath="{.spec.ports[0].nodePort}" services my-apache)
  export NODE_IP=$(kubectl get nodes --namespace default -o jsonpath="{.items[0].status.addresses[0].address}")
  echo http://$NODE_IP:$NODE_PORT
  ```

- **With Ingress**:
  Configure DNS or `/etc/hosts` for the host defined in `values.yaml`.

---

## 🛠 Uninstalling the Chart

```bash
helm uninstall my-apache
```

---

## 📜 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

## ✨ Author

- **Gaurav Singh** — Kubernetes & Helm Enthusiast  
