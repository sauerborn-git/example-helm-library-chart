# example chart using the library

An example helm chart containing a Deployment which includes a named template from a helm library chart

To test it first update the dependency
```
helm dependency update
```

Then you can test template it 
```
helm install examplechart . --dry-run --debug
```

If everything looks good you can install it:
```
helm install examplechart .
```

This example then creates a Deployment, where all the labels are set from the named template we included form the library, which should look similar to this:
```
kubectl describe  deployment examplechartusingthelibrary-deployment
Name:                   examplechartusingthelibrary-deployment
Namespace:              default
CreationTimestamp:      Thu, 22 Feb 2024 09:36:08 +0100
Labels:                 app.kubernetes.io/instance=examplechart
                        app.kubernetes.io/managed-by=Helm
                        app.kubernetes.io/name=examplechartusingthelibrary
                        app.kubernetes.io/version=1.16.0
                        helm.sh/chart=examplechartusingthelibrary-0.1.0
Annotations:            deployment.kubernetes.io/revision: 1
                        meta.helm.sh/release-name: examplechart
                        meta.helm.sh/release-namespace: default
Selector:               app.kubernetes.io/instance=examplechart,app.kubernetes.io/name=examplechartusingthelibrary
Replicas:               1 desired | 1 updated | 1 total | 1 available | 0 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  25% max unavailable, 25% max surge
Pod Template:
  Labels:  app.kubernetes.io/instance=examplechart
           app.kubernetes.io/managed-by=Helm
           app.kubernetes.io/name=examplechartusingthelibrary
           app.kubernetes.io/version=1.16.0
           helm.sh/chart=examplechartusingthelibrary-0.1.0
  Containers:
   examplechartusingthelibrary:
    Image:        nginx:1.16.0
    Port:         80/TCP
    Host Port:    0/TCP
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Conditions:
  Type           Status  Reason
  ----           ------  ------
  Available      True    MinimumReplicasAvailable
  Progressing    True    NewReplicaSetAvailable
OldReplicaSets:  <none>
NewReplicaSet:   examplechartusingthelibrary-deployment-5558f9bfc6 (1/1 replicas created)
Events:
  Type    Reason             Age   From                   Message
  ----    ------             ----  ----                   -------
  Normal  ScalingReplicaSet  3m8s  deployment-controller  Scaled up replica set examplechartusingthelibrary-deployment-5558f9bfc6 to 1
```