# Basics training 001 kubectl基礎編
---  
## 01: Confirm kubectl version
### Quiz.1: What information do you see?
### Quiz.2: Can you see both client and server?
```kubernetes-kubectl
kubectl version
```  
  
  
   
## 02: Getting kubernetes nodes information.
### Quiz.1: How many nodes are there?
### Quiz.2: What types of nodes are there?
```shell
kubectl get nodes
```  
   
   
   
## 03: Getting kubernetes pods information include system pods.
### Quiz.1: How many pods do you see?
### Quiz.2: Have you already placed a pod (container)?
```shell
kubectl get pods
``` 
   
   
   
## 04: Getting kubernetes pods information include system pods.
### Quiz.1: How many pods do you see?
### Quiz.2: Have you already placed a pod (container)?
```shell
kubectl get pods --all-namespaces
```  
   
   
    
## 05: Getting kubernetes namespaces.
### Quiz.1: What information do you see?
```shell
kubectl get ns
```
   
   
    
## 06: Creating your work namespaces.
### Quiz.1: Did the creation succeed?
```shell
kubectl create ns [YOUR_NAMESPACE_NAME]
```
> * insert unique your namespace name insted `[YOUR_NAMESPACE_NAME]`  
   
   
    
## 07: Deploy sample pods into your namespaces.
### Quiz.1: Did the creation succeed?
```shell
kubectl apply -f 01_deployment-nginx.yaml -n [YOUR_NAMESPACE_NAME]
```
   
   
   
## 08: Getting your pods information
### Quiz.1: How many pods do you see?
```shell
kubectl get pods
```   
        
        
        
## 09: Getting your pods information with namespaces
### Quiz.1: How many pods do you see?
```shell
kubectl get pods -n [YOUR_NAMESPACE_NAME]
```   
     
    
    
## 10: Setting your dedicated namespaces contexts as default.
### Quiz.1: Did the command succeed?
```shell
kubectl config set-context $(kubectl config current-context) --namespace=[YOUR_NAMESPACE_NAME]
```   
   
        
   
## 11: Getting your pods information with namespaces
### Quiz.1: How many pods do you see?
### Quiz.2: Can you view your deployed pods without namespace options?
```shell
kubectl get pods
```   
        
    
    
## 12: Getting your pods detail information.
### Quiz.1: What information do you see?
### Quiz.2: What is the pod namespace name?
### Quiz.3: On which node is the pod located?
### Quiz.4: What is the image of Pod?
### Quiz.5: What information does the event have?
```shell
kubectl describe pod [YOUR_POD_NAME]
```  
    
    
    
## 13: Deploy sample service into your namespaces.
### Quiz.1: Did the creation succeed?
```shell
kubectl apply -f ./02_service-nodeport-nginx.yaml
```
        
    
    
## 14: Getting your pods detail information.
### Quiz.1: What information do you see?
### Quiz.2: What is the Service namespace name?
### Quiz.3: What is the Service type?
### Quiz.4: What is NodePort number?
### Quiz.5: What is TargetPort number?
```shell
kubectl describe service [YOUR_CREATED_SERVICE_NAME]
```  
    
    
    
## 15: Getting a little detail your nodes, services.
### Quiz.1: What information do you see?
```shell
kubectl get nodes,svc -o wide

or

Node IP address information can also be confirmed from the Karbon UI.
 -1． Access the Karbon UI.
 -2． Select your cluster.
 -3． Select Nodes on the left vane.
 -4. Select Master or Worker.
```

## 16: Access your nginx via NodePort
### Quiz.1: Does the nginx default page been displayed successfully?
```
Access your Web-browser or curl command with master or worker nodes [IPAddress] + [NodePort]
```
> ( eg. `10.149.30.109:32114` ,This is sample URL. )
> Note: Replace IP with the IP address of your Master node or Worker node confirmed in steps 14 and 15.
> Note: Replace the port with the number of your NodePort confirmed in steps 14 and 15.
   
   
    
## 17: Getting logs from your pods.
### Quiz.1: What information do you see?
```shell
kubectl logs [YOUR_POD_NAME]
```  
   
   
    
## 18: Getting logs from your pods with tail mode.
### Quiz.1: Has the HTTP access log you accessed been displayed?
```shell
kubectl logs -f [YOUR_POD_NAME]

Access your Web-browser or curl command with master or worker nodes [IPAddress] + [NodePort]
after that
Access your Web-browser or curl command with master or worker nodes [IPAddress] + [NodePort]/aaaa

> ( eg. `10.149.30.109:32114` ,This is sample URL. )
> ( eg. `10.149.30.109:32114/aaaa` ,This is sample URL. )

```  
   
   
    
## 14: Scaling-out your sample app.
```shell
kubectl scale deployment nginx --replicas=4

or

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
kubectl delete service nginx-service
kubectl delete deployment nginx

or

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
