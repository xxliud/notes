```
helm install -f values.yaml --name my-release --namespace harbor harbor/harbor

helm del --purge my-release

kubectl get pvc -n harbor | awk 'NR>1{print $1}' | xargs kubectl delete pvc -n harbor

helm repo add harbor https://helm.goharbor.io
```

