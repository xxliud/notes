alter database database_name OWNER TO postgres;

create user postgres with password '123456';

alter user postgres superuser createrole createdb replication;



```shell
apiVersion: apps/v1
kind: Deployment
metadata:
  name: postgres
  namespace: base
  labels:
    app: postgres
spec:
  replicas: 1
  selector:
    matchLabels:
      app: postgres
  template:
    metadata:
      labels:
        app: postgres
    spec:
      containers:
      - name: postgres
        image: postgres:11.4
        imagePullPolicy: IfNotPresent
        ports:
        - containerPort: 5432
        env:
        #- name: POSTGRES_DB
        #  value: "gitlab_production"
        - name: POSTGRES_USER
          value: "gitlab"
        - name: POSTGRES_PASSWORD 
          value: "gitlab"
        resources:
          limits:
            cpu: 500m
            memory: 1024Mi
          requests:
            cpu: 500m
            memory: 1024Mi
        volumeMounts:
          - name: data
            mountPath: /var/lib/postgresql/data
      volumes:
        - name: data
          persistentVolumeClaim:
            claimName: postgres-project-pvc
```

```shell
apiVersion: v1
kind: Service
metadata:
  name: postgres
  namespace: redis
spec:
  ports:
    - name: http
      port: 5432
      protocol: TCP
      targetPort: 5432
  selector:
    app: postgres
```

