# kubernetes mongodb & mongo-express depl configuration


###  Starts a local Kubernetes cluster
if computer doesn't have VT-X/AMD-v enabled or Enabling it in the BIOS dosen't work add `--no-vtx-check`

```
minikube start --no-vtx-check --cpus='4' --memory='4000mb'
```
Gets the status of a local Kubernetes cluster

```
minikube status
```

### Creating MongoDB Secret 
create secret first using `kubectl apply -f mongodb-secret.yaml`, and check the secret `kubectl get secret`.
```
kubectl apply -f mongodb-secret.yaml
kubectl get secret
```

### Create MongoDB Deployment
create mongodb deployment and use the secret from before. use `kubectl get deployment` to check deployment.
```
kubectl apply -f mongodb-deployment.yaml
```

### Interact with MongoDB POD
use `kubectl get pod` to check pod status. to get detailed information on pod use `kubectl describe pod [pod-name]`. to get pods logs use `kubectl logs [pod-name]`.
```
kubectl get pod
kubectl describe pod [pod-name]
kubectl logs [pod-name]
```

### create MongoDB Service
```
kubectl apply -f mongodb-service.yaml
```

### create MongoDB ConfigMap
to make mongo-express interact with mongodb pod we need to get db url from mongodb-service and write it on configMap.
```
kubectl apply -f mongodb-config.yaml
```

### Create Mongo-Express Depl
create Mongo-Express deployment. we can use the same secret like mongodb and use db url from created configMap before. use `kubectl get deployment` to check deployment.
```
kubectl apply -f mongo-express-deployment.yaml
```

### Interact with Mongo-Express POD
use `kubectl get pod` to check pod status. to get detailed information on pod use `kubectl describe pod [pod-name]`. to get pods logs use `kubectl logs [pod-name]`.
```
kubectl get pod
kubectl describe pod [pod-name]
kubectl logs [pod-name]
```
### create Mongo-Express Service
use type "LoadBalancer" builds on NodePort and creates an external load-balancer
```
kubectl apply -f mongodb-ex-service.yaml
```
