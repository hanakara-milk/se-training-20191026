# SE Team training
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
   
   
    
## 11: Gettign a little detail your nodes, services.
```shell
`kubectl get nodes,svc -o wide
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
   
   
    
## 15: Cleanup tiny-hands-on environment.
```shell
kubectl delete -f [YAML_FILE_NAME]
```  
   
   
    
## 16: Cleanup tiny-hands-on environment.
```shell
kubectl delete ns [YOUR_NAMESPACE_NAME]
```
> * insert your namespace name insted `[YOUR_NAMESPACE_NAME]`  
