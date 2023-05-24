helm repo add bitnami https://charts.bitnami.com/bitnami

helm repo add runix https://helm.runix.net

helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx

helm repo update

helm install nginx-ingress ingress-nginx/ingress-nginx --set controller.publishService.enabled=true

kubectl create namespace pgadmin-namespace

helm install postgres-pgadmin runix/pgadmin4 -f pgadmin-values.yml -n pgadmin-namespace --set env.contextPath=/pgadmin

kubectl create namespace postgres-namespace

helm install postgres-postgresql bitnami/postgresql --version 12.4.2 --namespace postgres-namespace

kubectl apply -f pgadmin-ingress.yml --namespace pgadmin-namespace

kubectl apply -f neighbook-api-ingress.yml --namespace neighbook-namespace

helm uninstall my-release -n pgadmin-namespace

helm upgrade postgres-pgadmin runix/pgadmin4 -f pgadmin-values.yml -n pgadmin-namespace

kubectl apply -f neighbook-api-ingress.yml --namespace neighbook-namespace

kubectl create -f neighbook-api-deployment.yml

kubectl apply -f neighbook-api-deployment.yml

helm repo add bitnami https://charts.bitnami.com/bitnami

helm show values bitnami/minio > minio-values.yml

kubectl create namespace minio-namespace

helm install minio bitnami/minio --version 12.6.0 -f minio-values.yml --namespace minio-namespace

helm upgrade my-minio bitnami/minio -f minio-values.yml --namespace minio-namespace
