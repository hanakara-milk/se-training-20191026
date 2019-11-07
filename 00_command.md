# SE Team training 001 kubectl基礎編
---
## 0: Getting SE Team training cluster kubeconfig
```shell
Connect POC#11 Karbon UI and download kubeconfig from "kubernetes-training" cluster.
```  
    
[POC11-Karbon]: https://10.149.11.42:7050
[Karbon UIを見る][POC11-Karbon]
`https://10.149.11.42:7050`  
  
  
  
## 1: Confirm kubectl version
```kubernetes-kubectl
kubectl version
```  
  
  
   
## 2: Getting kubernetes nodes information.
```shell
kubectl get nodes
```  
   
   
   
## 3: Getting kubernetes pods information include system pods.
```shell
kubectl get pods --all-namespaces
```  
   
   
    
## 4: Getting kubernetes namespaces.
```shell
kubect get ns
```
   
   
    
## 5: Creating your work namespaces.
```shell
kubectl create ns [YOUR_NAMESPACE_NAME]
```
> * insert uniq your namespace name insted `[YOUR_NAMESPACE_NAME]`  
   
   
    
## 6: Deploy sample pods into your namespaces.
```shell
kubectl apply -f 01_deployment-nginx.yaml -n [YOUR_NAMESPACE_NAME]
```
> * insert uniq your namespace name insted `[YOUR_NAMESPACE_NAME]`
   
   
    
## 7: Getting your pods information
```shell
kubectl get pods -n [YOUR_NAMESPACE_NAME]
```
> * insert your namespace name insted `[YOUR_NAMESPACE_NAME]`  
   
   
        
## 8: Setting your dedicated namespaces contexts.
```shell
kubectl config set-context $(kubectl config current-context) --namespace=[YOUR_NAMESPACE_NAME]
```
> * insert your namespace name insted `[YOUR_NAMESPACE_NAME]`  
   
   
    
## 9: Getting your pods detail information.
```shell
kubectl describe pod [YOUR_POD_NAME]
```  
   
   
      
## 10: Deploy sample service into your namespaces.
```shell
kubectl apply -f ./02_service-nodeport-nginx.yaml
```  
   
   
    
## 11: Getting a little detail your nodes, services.
```shell
kubectl get nodes,svc -o wide
```  
  
  
     
## 12: Access your nginx via NodePort
```
Access your Web-browser or curl command with master or worker nodes [IPAddress] + [NodePort]
```
> ( eg. `10.149.30.109:32114`)  
   
   
    
## 13: Getting logs from your pods.
```shell
kubectl logs [YOUR_POD_NAME]
```  

## 14: Scaling-out your sample app.
```shell
kubectl apply -f ./03_scaleup-nginx.yaml
```  
    
# SE Team Training 101 Self-Healing編
---
## 1: Check 4 pods are running and pick up the name of 1 pod. (like nginx-ABCDEFG)
```shell
kubectl get pods
```

## 2: Delete 1 pods
```shell
kubectl delete pod [POD_NAME_TO_BE_DELETED]
```

Quiz: How many Pods are running now? Why?

## 3: Check the number of pods
```shell
kubectl get pods
```

## 4: Delete the deployment and service
```shell
kubectl delete -f 02_service-nodeport-nginx.yaml
kubectl delete -f 03_scaleup-nginx.yaml
```

# SE Team Training 101 Rolling-update編
---
## 1: Create a deployment and a service
```shell
kubectl apply -f 04_deployment-color-app.yaml
```

## 2: Check the deployment, rs, pods and services
```shell
kubectl get all
```

## 3: Access your webapp-color application via NodePort
```
Access your Web-browser with master or worker nodes [IPAddress] + [NodePort]
```
> ( eg. `10.149.30.109:32114`)  
   
## 4: Check the deployment and identify the version of the application
```shell
kubectl describe deployment webapp-color
```

Quiz: What is the app version?

## 5: Update the version of the webapp-color application and check the status of the pod
```shell
kubectl apply -f 05_verup-color-app.yaml ; watch kubectl get pod
```

Quiz: How are the application pods updated?

## 6: Access your webapp-color application via NodePort
```
Access your Web-browser with master or worker nodes [IPAddress] + [NodePort]
```
> ( eg. `10.149.30.109:32114`)  

## 7: Delete your deployment and service
```shell
kubectl delete -f 05_verup-color-app.yaml
```

# SE Team Training 101 Configmap編
---
## 1: Create a configmap
```shell
kubectl apply -f 06_configmap-color-app-pink.yaml
```

## 2: Check the configmap
```shell
kubectl get cm appcolor
kubectl describe cm appcolor
```

## 3: Create a deployment
```shell
kubectl apply -f 07_deployment-color-app-latest.yaml
```

## 4: Check the deployment, rs, pods and services, pick up the name of the pod (like webapp-color-ABCDEFG)
```shell
kubectl get all
```

## 5: Check the environent variables from the Pod
```shell
kubectl exec -it [YOUR_POD_NAME] -- env
```

Quiz: What color will be your webpage?

## 6: Access your webapp-color application via NodePort
```
Access your Web-browser with master or worker nodes [IPAddress] + [NodePort]
```
> ( eg. `10.149.30.109:32114`)  

## 7: Delete and recreate the configmap
```shell
kubectl delete -f 06_configmap-color-app-pink.yaml
kubectl apply -f 08_configmap-color-app-blue.yaml
```

## 8: Check the configmap
```shell
kubectl get cm appcolor
kubectl describe cm appcolor
```

## 9: Delete and recreate the deployment
```shell
kubectl delete -f 07_deployment-color-app-latest.yaml
kubectl apply -f 07_deployment-color-app-latest.yaml
```

## 10: Check the deployment, rs, pods and services, pick up the name of the pod (like webapp-color-ABCDEFG)
```shell
kubectl get all
```

## 11: Check the environent variables from the Pod
```shell
kubectl exec -it [YOUR_POD_NAME] -- env
```

Quiz: What color will be your webpage?

## 12: Access your webapp-color application via NodePort
```
Access your Web-browser with master or worker nodes [IPAddress] + [NodePort]
```

## 13: Delete the configmap and deployment 
```shell
kubectl delete -f 07_deployment-color-app-latest.yaml
kubectl delete -f 08_configmap-color-app-blue.yaml
```
