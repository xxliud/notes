```shell
# redis pvc
---
apiVersion: v1
kind: PersistentVolume
metadata:
  name: redis-project-pv
  namespace: base
  labels:
    pv: redis-project-pv
spec:
  capacity:
    storage: 1Gi
  accessModes:
  - ReadWriteOnce
  persistentVolumeReclaimPolicy: Recycle
  hostPath:
    path: /data

---
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: redis-project-pvc
  namespace: base
spec:
  accessModes:
  - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
  selector:
    matchLabels:
      pv: redis-project-pv
      
      
      
# postgres pvc   
---
apiVersion: v1
kind: PersistentVolume
metadata:
  name: postgres-project-pv
  namespace: base
  labels:
    pv: postgres-project-pv
spec:
  capacity:
    storage: 1Gi
  accessModes:
  - ReadWriteOnce
  persistentVolumeReclaimPolicy: Recycle
  hostPath:
    path: /data

---
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: postgres-project-pvc
  namespace: base
spec:
  accessModes:
  - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
  selector:
    matchLabels:
      pv: postgres-project-pv
```



```
docker run --privileged -d                          \
  -v /Users/xingxu/workspace/nfs:/nfs                        \
  -e NFS_EXPORT_0='/nfs  (rw,insecure,no_subtree_check,no_root_squash,fsid=1)'  \
  -p 2049:2049   -p 2049:2049/udp   \
  -p 1111:111     -p 1111:111/udp     \
  -p 32765:32765 -p 32765:32765/udp \
  -p 32767:32767 -p 32767:32767/udp \
  erichough/nfs-server
  
  
  docker run -d --privileged  \
-v /Users/xingxu/workspace/nfs:/nfs \
-e NFS_EXPORT_DIR_1=/nfs \
-e NFS_EXPORT_DOMAIN_1=\* \
-e NFS_EXPORT_OPTIONS_1=rw,insecure,no_subtree_check,no_root_squash,fsid=1 \
-p 111:111 -p 111:111/udp \
-p 2049:2049 -p 2049:2049/udp \
-p 32765:32765 -p 32765:32765/udp \
-p 32766:32766 -p 32766:32766/udp \
-p 32767:32767 -p 32767:32767/udp \
fuzzle/docker-nfs-server:latest
```

