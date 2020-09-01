# Translation 1

## Course: Architecting with Google Kubernetes Engine - Foundations
### Module: Kubernetes Architecture

1.  __AK8S-03 Creating a GKE Cluster via GCP Console__

- Use the GCP Console to build and manipulate GKE clusters

__Task 1. Deploy GKE clusters__
  Create cluster on `us-central1-a` zone
    
 ```
  gcloud container clusters create standard-cluster-1 \
  --zone us-central1-a

  ```
  __Task 2. Modify GKE clusters__
  
  Increase size of the cluster from 3 to 4
  
```
gcloud container clusters resize standard-cluster-1 \
--zone us-central1-a \
--node-pool default-pool \
--num-nodes 4

```

 __Task 3. Deploy a sample workload__
 
 open your cloud shell and edit the file using `nano`:
 ```
 nano nginx-deployment.yaml
 
 ```
 and copy the code below
 ```
 ---
apiVersion: "apps/v1"
kind: "Deployment"
metadata:
  name: "nginx-1"
  namespace: "default"
  labels:
    app: "nginx-1"
spec:
  replicas: 3
  selector:
    matchLabels:
      app: "nginx-1"
  template:
    metadata:
      labels:
        app: "nginx-1"
    spec:
      containers:
      - name: "nginx-1"
        image: "nginx:latest"
---
apiVersion: "autoscaling/v2beta1"
kind: "HorizontalPodAutoscaler"
metadata:
  name: "nginx-1-hpa-ucyn"
  namespace: "default"
  labels:
    app: "nginx-1"
spec:
  scaleTargetRef:
    kind: "Deployment"
    name: "nginx-1"
    apiVersion: "apps/v1"
  minReplicas: 1
  maxReplicas: 5
  metrics:
  - type: "Resource"
    resource:
      name: "cpu"
      targetAverageUtilization: 80

 ```
 after copying press __CTRL + O__, __ENTER__ then lastly __CTRL + X__ to exit
 
 Login into the cluster
 ```
 gcloud container clusters get-credentials standard-cluster-1 \
 --zone us-central1-a
 
 ```
 
 Deploy your workload
 ```
 kubectl apply -f nginx-deployment.yaml
 ```
 Display information about the Deployment
 ```
 kubectl describe deployment nginx-1
 ```
 Check deployed workload
 ```
 kubectl get pods -l app=nginx-1
 ```
 Display information about a Pod:
 ```
 kubectl describe pod <pod-name>
 ```