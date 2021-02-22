本地启动minikube

```shell
minikube start --cpus=5 --memory=9196 --driver=virtualbox --registry-mirror=https://registry.docker-cn.com --disk-size=50000mb
```



Helm

```
helm init -i registry.cn-hangzhou.aliyuncs.com/google_containers/tiller:v2.16.12 --stable-repo-url http://mirror.azure.cn/kubernetes/charts/ --service-account tiller --override spec.selector.matchLabels.'name'='tiller',spec.selector.matchLabels.'app'='helm' --output yaml | sed 's@apiVersion: extensions/v1beta1@apiVersion: apps/v1@' | kubectl apply -f -





apiVersion: v1
kind: ServiceAccount
metadata:
  name: tiller
  namespace: kube-system
---
apiVersion: rbac.authorization.k8s.io/v1beta1
kind: ClusterRoleBinding
metadata:
  name: tiller
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
  - kind: ServiceAccount
    name: tiller
    namespace: kube-system
```





```shell
# 批量删除pvc
kubectl get pvc -n harbor | awk 'NR>1{print $1}' | xargs kubectl delete pvc -n harbor
```

