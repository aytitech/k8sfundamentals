# Prometheus Kubernetes Stack

-- Prometheus Kubernetes Stack: https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-prometheus-stack

-- Prometheus Kubernetes Operator: https://prometheus-operator.dev/

* Namespace oluştur

```
$ kubectl create namespace monitoring
```

* kube-prometheus-stack kur

```
$ helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
$ helm repo update
$ helm install kubeprostack --namespace monitoring prometheus-community/kube-prometheus-stack
```

* Prometheus'u kontrol et

```
$ kubectl --namespace monitoring port-forward svc/kubeprostack-kube-promethe-prometheus 9090
```

queries:
Şu ana kadar oluşturulmuş tüm podlar: ```kube_pod_created```

Namespace'e göre dağılım ^^:```count by (namespace) (kube_pod_created)```

Mevcut çalışan podlar: ```sum by (namespace) (kube_pod_info)```

Ready durumunda olmayan podlar "namespace'e göre dağılım": ```sum by (namespace) (kube_pod_status_ready{condition="false"})```

* Alert manager kontrol et

```
kubectl --namespace monitoring port-forward svc/kubeprostack-kube-promethe-alertmanager 9093   
```

* Grafana'a bağlan

```
kubectl --namespace monitoring port-forward svc/kubeprostack-grafana 8080:80
```
username: admin

password: prom-operator

```
kubectl get secret kubeprostack-grafana -n monitoring -o jsonpath="{.data.admin-password}" | base64 --decode ; echo  
```

**Grafana Dashboards:** https://grafana.com/grafana/dashboards/ 


