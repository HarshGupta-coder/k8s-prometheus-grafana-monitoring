# k8s-prometheus-grafana-monitoring
Monitor your Kubernetes cluster and pipelines with Prometheus and Grafana. This repository provides a comprehensive guide and configurations for setting up robust monitoring solutions for your Kubernetes environment.

# Kubernetes Monitoring with Prometheus and Grafana

This project provides a step-by-step guide to set up monitoring for a Kubernetes cluster and pipelines using Prometheus and Grafana.

## Requirements

Make sure you have the following tools installed on your system:

- [Minikube](https://minikube.sigs.k8s.io/docs/start/)
- [Helm](https://helm.sh/docs/intro/install/)

## Steps

### 1. Start Minikube

```bash
minikube start
```
![image](https://github.com/HarshGupta-coder/k8s-prometheus-grafana-monitoring/assets/54001485/8db62ea5-4af3-4bda-bbab-87419a43b1d3)

### 2. List Available Pods

```bash
kubectl get pod -A
```
![image](https://github.com/HarshGupta-coder/k8s-prometheus-grafana-monitoring/assets/54001485/00e1cc1b-4a37-4cf9-ad26-fec95ffc44ee)

### 3. Install Prometheus

#### 3.1 Add Helm Repo

```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
```

#### 3.2 Update Helm Repo

```bash
helm repo update
```

#### 3.3 Install Prometheus

```bash
helm install prometheus prometheus-community/prometheus
```

### 4. Expose Prometheus Service

```bash
kubectl expose service prometheus-server --type=NodePort --target-port=9090 --name=prometheus-server-ext
```

### 5. Access Prometheus

Get Minikube IP:

```bash
minikube ip
```

Access Prometheus at: `http://[minikube ip]:[prometheus nodeport]`

### 6. Install Grafana

#### 6.1 Add Helm Repo

```bash
helm repo add grafana https://grafana.github.io/helm-charts
```

#### 6.2 Update Helm Repo

```bash
helm repo update
```

#### 6.3 Install Grafana

```bash
helm install grafana grafana/grafana
```

### 7. Expose Grafana Service

```bash
kubectl expose service grafana --type=NodePort --target-port=3000 --name=grafana-ext
```

### 8. Access Grafana

Get Minikube IP:

```bash
minikube ip
```

Access Grafana at: `http://[minikube ip]:[grafana nodeport]`

Get Grafana Admin Password:

```bash
kubectl get secret --namespace default grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
```
![image](https://github.com/HarshGupta-coder/k8s-prometheus-grafana-monitoring/assets/54001485/f714d310-1849-4aab-a93e-a39d3377bed1)

### 9. Connect Grafana to Prometheus

- Access Grafana webpage.
- Go to Data Sources > Add a Prometheus data source.
- Enter Prometheus URL: `[minikube ip]:[prometheus nodeport]`.
- Click Save & Test.

### 10. Import Grafana Dashboard

- Import a basic dashboard with code "3662".
- Connect it to the Prometheus data source.
![image](https://github.com/HarshGupta-coder/k8s-prometheus-grafana-monitoring/assets/54001485/17604d07-ac0a-4bd3-894b-df62f3c76b8f)
![image](https://github.com/HarshGupta-coder/k8s-prometheus-grafana-monitoring/assets/54001485/0e0705c1-3bc5-424a-a2b1-85d35445e2a0)

### 11. Basic Prometheus Queries

Example Query:

```bash
kube_deployment_status_replicas{namespace="default",deployment="prometheus-server"}
```
![image](https://github.com/HarshGupta-coder/k8s-prometheus-grafana-monitoring/assets/54001485/5dbd35d3-e7cd-4a98-bc82-5e3777a4a82e)

### 12. Conclusion

Your Kubernetes cluster and pipelines are now monitored using Prometheus and Grafana. Customize the dashboards and alerts based on your specific needs.
```

Copy and paste this content into your `README.md` file in your GitHub repository.
