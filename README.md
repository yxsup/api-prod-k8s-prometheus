###直接用目录升级

helm upgrade kube-prometheus-stack \
  /root/k8s-prometheus/chart-src/kube-prometheus-stack \
  -n monitoring \
  -f /root/k8s-prometheus/prometheus-values.yaml \
  --description "remove AIX dashboard"


###查看结果
helm list -n monitoring
helm history kube-prometheus-stack -n monitoring
kubectl get pods -n monitoring

必要时重启 Grafana，让 provisioned Dashboard 重新加载：

kubectl rollout restart deployment/kube-prometheus-stack-grafana -n monitoring
kubectl rollout status deployment/kube-prometheus-stack-grafana -n monitoring
