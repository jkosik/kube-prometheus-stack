# kube-prometheus-stack & Prometheus for k8s workloads
This projects deploys prefabrikated `kube-prometheus-stack` into the k8s cluster. [values-custom.yaml](values-custom.yaml) modifies default settings, e.g. Grafana scraping metrics from Prometheus directly via SVC url, custom ServiceMonitors, custom alertin rules,...

## Deployment
1. Create custom [values-custom.yaml](values-custom.yaml) to override default [Helm Chart values](https://github.com/prometheus-community/helm-charts/blob/main/charts/kube-prometheus-stack/values.yaml).
2. Add to your deployment pipeline:
```
kubectl create ns monitoring

helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
helm search repo prometheus-community/kube-prometheus-stack --versions | head

helm upgrade --install -f values-custom.yaml monitoring prometheus-community/kube-prometheus-stack --version 16.13.0 -n monitoring
```

## Additional info
- Default Grafana credentials: admin/prom-operator
- `kubectl deploy -f prometheus-dummy-exporter.yaml -n YOURNAMESPACE` and update `additionalServiceMonitors` in [values-custom.yaml](values-custom.yaml) to start scraping own metrics.
- updating grafana.sidecar.datasources.url require Grafana Pod restart