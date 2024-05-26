# Installer Helm 3 #
curl -o helm-v3.10.3-linux-amd64.tar.gz https://get.helm.sh/helm-v3.10.3-linux-amd64.tar.gz
# Modifier les permissions
chmod 777 helm-v3.10.3-linux-amd64.tar.gz
# Extraire les fichiers
tar -zxvf helm-v3.10.3-linux-amd64.tar.gz  <br>
mv linux-amd64/helm /usr/local/bin/helm  <br>
ll /usr/local/bin/helm <br>
chmod +x /usr/local/bin/helm <br>
echo $PATH <br>
export PATH=$PATH:/usr/local/bin
# Vérifier la version de Helm
helm version
# Installer Prometheus et Grafana #
# Ajouter le dépôt Helm pour les charts Prometheus
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts <br>
helm repo add stable https://charts.helm.sh/stable <br>
# Mettre à jour les dépôts Helm pour s'assurer que nous avons la dernière version des charts disponibles
helm repo update
# Créer un namespace 'monitoring' 
kubectl create namespace monitoring
# Installer la stack Prometheus-Kube via Helm dans le namespace 'monitoring'
helm install prometheus prometheus-community/kube-prometheus-stack --namespace monitoring
# Vérifier les pods déployés dans le namespace 'monitoring'
kubectl get pods --namespace=monitoring
# Éditer le service Grafana 
kubectl edit svc --namespace monitoring prometheus-grafana
# Éditer le service Prometheus
kubectl edit svc --namespace monitoring prometheus-kube-prometheus-prometheus
