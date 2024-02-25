# Deploy apisix with helm

## Prerequisites


## Install apisix with helm

```bash
helm repo add apisix https://charts.apiseven.com
helm repo update
helm install apisix apisix/apisix --create-namespace  --namespace apisix
```

## install apisix dashboard with helm

```bash
helm install apisix-dashboard apisix/apisix-dashboard --namespace apisix

export POD_NAME=$(kubectl get pods --namespace apisix -l "app.kubernetes.io/name=apisix-dashboard,app.kubernetes.io/instance=apisix-dashboard" -o jsonpath="{.items[0].metadata.name}")
export CONTAINER_PORT=$(kubectl get pod --namespace apisix $POD_NAME -o jsonpath="{.spec.containers[0].ports[0].containerPort}")
echo "Visit http://127.0.0.1:8080 to use your application"
kubectl --namespace apisix port-forward $POD_NAME 8080:$CONTAINER_PORT
```

