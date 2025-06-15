
# CI/CD with GitHub Actions, Terraform, and EKS

This project demonstrates how to:
- Provision AWS infrastructure using Terraform
- Deploy a Node.js app to EKS with Helm
- Secure pipelines with Trivy and tfsec
- Automate CI/CD using GitHub Actions

📌 Tools Used: Terraform, EKS, GitHub Actions, Docker, Helm, Trivy and tfsec

#Monitoring and Cost Tracking (Manual Setup)

Prometheus & Grafana (install with Helm)
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
helm install monitoring prometheus-community/kube-prometheus-stack \
  --namespace monitoring --create-namespace

Access Grafana:
kubectl port-forward svc/monitoring-grafana -n monitoring 3000:80

Login:
User: admin
Password: prom-operator (change after first login)

Kubecost (install with Helm):
helm repo add kubecost https://kubecost.github.io/cost-analyzer/
helm repo update
helm install kubecost kubecost/cost-analyzer \
  --namespace kubecost --create-namespace \
  --set kubecostToken="YOUR_TOKEN" \
  --set global.prometheus.enabled=false \
  --set global.prometheus.fqdn="http://monitoring-prometheus.monitoring:9090" 

  Access Kubecost UI:
  kubectl port-forward --namespace kubecost svc/kubecost-cost-analyzer 9090:9090


