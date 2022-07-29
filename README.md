- [Reference](https://www.containiq.com/post/deploy-redis-cluster-on-kubernetes)

### Build Service

```bash
kubectl create ns redis

kubectl apply -f sc.yaml
kubectl apply -f pv.yaml

kubectl apply -n redis -f redis-config.yaml
# kubectl get configmap -n redis

kubectl apply -n redis -f redis-statefulset.yaml
# kubectl get pods -n redis

# Headless Serveice.
# (Headless service means that only internal pods can communicate with each other.
#  They are not exposed to external requests outside of the Kubernetes cluster.)
kubectl apply -n redis -f redis-service.yaml
# kubectl get service -n redis
```

### Check Replication

```bash
kubectl -n redis logs redis-0
kubectl -n redis describe pod redis-0
kubectl -n redis exec -it redis-0 -- sh
# redis-cl
# auth a-very-complex-password-here
# info replication
```

### Test Replication

```bash
kubectl -n redis exec -it redis-0 -- sh
redis-cli
auth a-very-complex-password-here

SET emp1 raja
SET emp2 mano
SET emp3 ram
```
