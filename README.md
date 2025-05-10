
# 🚀 Flask Rental App – Helm Chart Deployment on Kubernetes

This project provides a production-ready Helm chart for deploying a **Flask-based rental application** (e.g. car rental system) with a **MySQL database** backend on a Kubernetes cluster.  
The architecture follows **cloud-native principles** using Docker, Helm, and Kubernetes manifests for scalability and modularity.

---

## 🧱 Project Structure

```
flask-rental-helm-chart/
├── Chart.yaml
├── values.yaml
├── templates/
│   ├── app-deployment.yaml
│   ├── app-service.yaml
│   ├── app-secret.yaml
│   ├── app-configmap.yaml
│   ├── db-deployment.yaml
│   ├── db-service.yaml
│   ├── db-secret.yaml
│   ├── db-configmap.yaml
│   ├── db-pv.yaml
│   ├── db-pvc.yaml
│   ├── ingress.yaml
│   └── namespace.yaml
└── .helmignore
```

> **Note**: This project includes raw Kubernetes manifests. You can customize and convert them into a Helm chart under the `templates/` directory. An example `.tgz` chart is included in `helm-s3-repo-tar-file/`.

---

## ⚙️ Prerequisites

- Docker installed
- A Kubernetes cluster (Minikube, EKS, GKE, etc.)
- Helm CLI installed
- AWS CLI (optional, for S3 chart hosting)
- Your Flask app Docker image pushed to a remote registry (e.g. Docker Hub)

---

## 📸 Docker Image Build & Push

```bash
# Build the image
docker build -t edzalpbrn/rental-app:latest .

# Push to Docker Hub (or your preferred registry)
docker push edzalpbrn/rental-app:latest
```

---

## 📦 Packaging the Helm Chart

```bash
# Navigate to chart directory
cd flask-rental-helm-chart

# Check chart validity
helm lint .

# Package the chart
helm package .
```

Output:
```
flask-rental-helm-chart-0.1.0.tgz
```

---

## 🪣 Upload Chart to S3 (Optional)

```bash
aws s3 cp flask-rental-helm-chart-0.1.0.tgz s3://your-bucket-name/helm/
```

You can then use it as a Helm repo:

```bash
helm repo add rentalapp https://s3.amazonaws.com/your-bucket-name/helm/
helm repo update
```

---

## 🚀 Install the Helm Chart

From S3 repo:
```bash
helm install rental-backend rentalapp/flask-rental-helm-chart
```

Or locally:
```bash
helm install rental-backend ./flask-rental-helm-chart
```

---

## 📄 Example Ingress Configuration

```yaml
rules:
  - host: rental.erkanbaran.me
    http:
      paths:
        - path: /
          pathType: Prefix
          backend:
            service:
              name: flask-service
              port:
                number: 8000
```

---

## 📈 Benefits

- Modular and reusable chart
- Clean Helm structure with ConfigMaps and Secrets
- Fully containerized 3-tier cloud-native architecture
- S3-based distribution ready

---

## 👤 Author

**Erkan Baran**  
DevOps | Cloud Technologies  
📧 erkan@example.com  
🌐 erkanbaran.me

---

## 📝 License

MIT License – feel free to use and modify.
