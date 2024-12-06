KIND_EXPERIMENTAL_PROVIDER=podman        
kind create cluster

install prometheus and grafana

helm install prometheus prometheus-community/prometheus \
  --namespace monitoring \
  --values prometheus-values.yaml

helm install grafana grafana/grafana \
  --namespace monitoring \
  --values grafana-values.yaml

port forward services

kubectl port-forward -n monitoring svc/prometheus-server 9090:80

kubectl port-forward -n monitoring svc/grafana 3000:80

Troubleshooting

check if pods are pending, service exists, pods are running, service endpoints, prometheus can't scrape targets, etc

kubectl describe pods -n monitoring
kubectl get svc -n monitoring
kubectl get pods -n monitoring
kubectl get endpoints -n monitoring
kubectl get configmap -n monitoring
kubectl describe configmap prometheus-server -n monitoring

