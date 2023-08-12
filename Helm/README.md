helm repo add bitnami https://charts.bitnami.com/bitnami

helm repo add runix https://helm.runix.net

helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx

helm repo add grafana https://grafana.github.io/helm-charts

helm repo update

helm install nginx-ingress ingress-nginx/ingress-nginx --set controller.publishService.enabled=true

kubectl create namespace pgadmin-namespace

helm install postgres-pgadmin runix/pgadmin4 -f pgadmin-values.yml -n pgadmin-namespace --set env.contextPath=/pgadmin

helm upgrade postgres-pgadmin runix/pgadmin4 -f pgadmin-values.yml -n pgadmin-namespace --set env.contextPath=/pgadmin

kubectl create namespace postgres-namespace

helm install postgres-postgresql bitnami/postgresql --version 12.4.2 --namespace postgres-namespace

kubectl apply -f pgadmin-ingress.yml --namespace pgadmin-namespace

kubectl apply -f neighbook-api-ingress.yml --namespace neighbook-namespace

helm uninstall my-release -n pgadmin-namespace

helm upgrade postgres runix/pgadmin4 -f pgadmin-values.yml -n pgadmin-namespace

kubectl apply -f neighbook-api-ingress.yml --namespace neighbook-namespace

kubectl create -f neighbook-api-deployment.yml

kubectl apply -f neighbook-api-deployment.yml

helm repo add bitnami https://charts.bitnami.com/bitnami

helm show values bitnami/minio > minio-values.yml

kubectl create namespace minio-namespace

helm install minio bitnami/minio --version 12.6.0 -f minio-values.yml --namespace minio-namespace

helm upgrade minio bitnami/minio -f minio-values.yml --namespace minio-namespace

kubectl apply -f certificat-ressources.yml

helm repo add ory https://k8s.ory.sh/helm/charts

helm repo update

helm show values ory/kratos > kratos-values.yml

helm show values bitmani/postgresql > postgresql-values.yml

helm install nginx-ingress-sam ingress-nginx/ingress-nginx --set controller.publishService.enabled=true --namespace minio-namespace

kubectl create namespace kratos-namespace

helm install kratos ory/kratos -f kratos-values.yml --namespace kratos-namespace

kubectl apply -f kratos-admin-ingress.yml --namespace kratos-namespace
kubectl apply -f kratos-public-ingress.yml --namespace kratos-namespace

kubectl create namespace selfservice-ui-namespace

helm install kratos-selfservice-ui ory/kratos-selfservice-ui-node -f kratos-selfservice-ui-values.yml --namespace selfservice-ui-namespace

helm upgrade kratos-selfservice-ui ory/kratos-selfservice-ui-node -f kratos-selfservice-ui-values.yml --namespace selfservice-ui-namespace

kubectl apply -f kratos-selfservice-ui-ingress.yml

kubectl apply -f minio-ingress.yml

helm show values ory/kratos-selfservice-ui-node > kratos-selfservice-ui-values.yml

helm upgrade kratos ory/kratos -f kratos-values.yml --namespace kratos-namespace

helm upgrade kratos-selfservice-ui ory/kratos-selfservice-ui-node -f kratos-selfservice-ui-values.yml --namespace selfservice-ui-namespace

kubectl apply -f kratos-admin-ingress.yml

helm show values ory/oathkeeper > oathkeeper-values.yml

kubectl create namespace oathkeeper-namespace

helm install oathkeeper ory/oathkeeper -f oathkeeper-values.yml --set-file=oathkeeper.accessRules=./rules.json --namespace oathkeeper-namespace

helm upgrade oathkeeper ory/oathkeeper -f oathkeeper-values.yml --set-file=oathkeeper.accessRules=./rules.json --set-file oathkeeper.mutatorIdTokenJWKs=./jwks.json --namespace oathkeeper-namespace

kubectl apply -f grafana.yml

helm show values grafana/grafana > grafana-values.yml

kubectl apply -f neighbook-marketplace-api-deployment.yml
kubectl apply -f oathkeeper-ingress.yml
kubectl apply -f oathkeeper-api-ingress.yml

kubectl apply -f ridepal-journey-api-deployment.yml

docker run oryd/oathkeeper:v0.40.6 credentials generate --alg RS256 > jwks.json