## Role binding

```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: kube-admin
  namespace: kube-system

---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: admin-binding
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
- kind: ServiceAccount
  name: kube-admin
  namespace: kube-system
```

##  Secret Token

```bash
$ kubectl -n kube-system describe secret $(kubectl -n kube-system get secret | grep kube-admin | awk '{print $1}')
Name:         kube-admin-token-5r76l
Namespace:    kube-system
Labels:       <none>
Annotations:  kubernetes.io/service-account.name: kube-admin
              kubernetes.io/service-account.uid: 09c87293-443d-4dcf-9569-3e6fc14b5fa0

Type:  kubernetes.io/service-account-token

Data
====
ca.crt:     1099 bytes
namespace:  11 bytes
token:      eyJhbGc__xxx__yuUaY0D7l5B2A

```

## Start proxy

```bash
$ kubectl get svc -n kubernetes-dashboard
NAME                        TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)        AGE
dashboard-metrics-scraper   ClusterIP   10.40.183.41   <none>        8000/TCP       19h
kubernetes-dashboard        NodePort    10.40.73.252   <none>        443:4895/TCP   19h

$ kubectl proxy
Starting to serve on 127.0.0.1:8001
```

## Get url: https://192.168.212.48:4895

