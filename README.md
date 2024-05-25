# Installer Helm 3 #
curl -o helm-v3.10.3-linux-amd64.tar.gz https://get.helm.sh/helm-v3.10.3-linux-amd64.tar.gz \n
chmod 777 helm-v3.10.3-linux-amd64.tar.gz
tar -zxvf helm-v3.10.3-linux-amd64.tar.gz
helm version --template='Version: {{.Version}}'
# Installer Prometheus et Grafana #
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts 
helm repo update
kubectl create namespace monitoring
helm install prometheus prometheus-community/kube-prometheus-stack --namespace monitoring
kubectl get pods --namespace=monitoring
kubectl edit svc --namespace monitoring prometheus-grafana
kubectl edit svc --namespace monitoring prometheus-kube-prometheus- prometheus
