本地启动minikube

```shell
# 启动minikube 使用国内镜像源
minikube start --cpus=5 --memory=9196 --disk-size=50000mb --vm-driver=virtualbox  --registry-mirror=https://registry.docker-cn.com --registry-mirror=https://8eoqixdq.mirror.aliyuncs.com --registry-mirror=https://dockerhub.azk8s.cn  --image-repository=registry.cn-hangzhou.aliyuncs.com/google_containers

# 挂载卷轴
minikube mount /Users/xingxu/workspace/k8s/pv:/data

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





2021年划计

```markdown
* 全年开支明细
- 房贷 3.2w
- 保险 0.85w
- 生活费 6w
- 孩子 1.5w

```

