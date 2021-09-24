
## 1

***Create container reg secret***

Run below command

```
kubectl create secret docker-registry acr-regcred --docker-server=anahidcalcacr.azurecr.io --docker-username=xxxxxxxxxx --docker-password=xxxxxxxxxxxx --docker-email=anahid@vmware.com
```

## 2

- Create Service Account (associated with imagepullsecret acr-regcred)
- Create ClusterRole to use vmware-system-priviledged (default psp)
- Create ClusterRoleBinding to allow all service accounts to use the clusterrole

```
kubectl apply -f psp.yaml
```

## 3


Create 
- deployment definition of the workload
- associate the deployment template with newly create service account ---> so that 
    - k8s knows how to pull the image (auth to pvt registry)
    - it ensures that deployment has permission to spin up pods for downloaded container, create service etc
- create service to expose the workload

Create deployment of the sample app

```
kubectl apply -f deployment.yaml
```


## Handy commands

```
kubectl get events --sort-by='.metadata.creationTimestamp' -A
```