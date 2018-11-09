# webui_heapster_rbac
How to install the web ui - heapster - dashboard admin with rbac
```
kubectl create -f https://raw.githubusercontent.com/kubernetes/kops/master/addons/kubernetes-dashboard/v1.8.3.yaml

kubectl create -f https://raw.githubusercontent.com/kubernetes/kops/master/addons/monitoring-standalone/v1.7.0.yaml

kubectl proxy

http://localhost:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/#!/deploy/app?namespace=default
```

# Create the service account in the current namespace
# (we assume default)
```
kubectl create serviceaccount my-dashboard-sa
```
# Give that service account root on the cluster
```
kubectl create clusterrolebinding my-dashboard-sa \
 --clusterrole=cluster-admin \
 --serviceaccount=default:my-dashboard-sa
```
# Find the secret that was created to hold the token for the SA
```
kubectl get secrets
```
# Show the contents of the secret to extract the token
```
kubectl describe secret my-dashboard-sa-token-xxxxx
```
