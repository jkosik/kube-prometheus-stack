# kube-prometheus-stack & Prometheus for k8s workloads
This projects deploys prefabrikated `kube-prometheus-stack` into the k8s cluster. `custom-values.yaml` modifies default settings, e.g. Grafana scraping metrics from Prometheus via SVC url or adding custom ServiceMonitors.

## Deployment
1. Mirror https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-prometheus-stack to `kube-prometheus-stack/` directory.
2. Create custom `values-custom.yaml` to override defaults.
3. From `kube-prometheus-stack/` run `helm dependency update` which downloads Helm dependency packages to `kube-prometheus-stack/charts`
4. From root: `helm install -f values-custom.yaml prom-k8s kube-prometheus-stack/`

Default Grafana credentials: admin/prom-operator
