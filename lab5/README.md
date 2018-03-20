###Step 1
```
kubectl cluster-info
kubectl get nodes
```
### Step 2
```
kubectl create -f redis-master-controller.yaml
kubectl get rc
kubectl get pods
```
### Step 3
```
kubectl create -f redis-master-service.yaml
kubectl get services
kubectl describe services redis-master
```
### Step 4
```
kubectl create -f redis-slave-controller.yaml
kubectl get rc
```
### Step 5
```
kubectl create -f redis-slave-service.yaml
kubectl get services
```
### Step 6
```
kubectl create -f frontend-controller.yaml
kubectl get rc
kubectl get pods
```
### Step 7
```
kubectl create -f frontend-service.yaml
kubectl get services
```
### Step 8
```
kubectl get pod
kubectl describe service frontend | grep NodePort
```