### Install<img src="/Users/jason/Library/Application Support/typora-user-images/image-20220622093715304.png" alt="image-20220622093715304" style="zoom:150%;" />

```java
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.6.0/aio/deploy/recommended.yaml
```

```java
kubectl proxy
```

```ja
http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/
```



[ubernetes](https://github.com/kubernetes)/**[dashboard](https://github.com/kubernetes/dashboard)**:

```java
vim dashboard-adminuser.yaml
```

```java
apiVersion: v1
kind: ServiceAccount
metadata:
  name: admin-user
  namespace: kubernetes-dashboard
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: admin-user
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
- kind: ServiceAccount
  name: admin-user
  namespace: kubernetes-dashboard
```

```java
kubectl -n kubernetes-dashboard create token admin-user
```



