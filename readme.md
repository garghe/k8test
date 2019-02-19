## How to setup a local Kubernets using Minikube


#### Setup Minikube

1. brew cask install minikube_

2. brew install kubernetes-cli

3. kubectl config use-context minikube

4. kubectl cluster-info

5. minikube dashboard


#### Create a simple NodeJS app

Server.js:

```var http = require(‘http’);
   var handleRequest = function(request, response) {
   console.log(‘Received request for URL: ‘ + request.url);
   response.writeHead(200);
   response.end(‘Hello Medium!’);
   };
   var www = http.createServer(handleRequest);
   www.listen(8080);
 ```
   
       
eval $(minikube docker-env)   - to UNDO: eval $(minikube docker-env -u).


#### Build container
docker build -t hello-node:v1 .


#### Create a deployment: 
kubectl run hello-node --image=hello-node:v1 --port=8080 --image-pull-policy=Never

#### Show Deployments:
kubectl get deployments

#### View Pods:
kubectl get pods

#### View Config:
kubectl config view

#### Expose Service:
kubectl expose deployment hello-node --type="LoadBalancer"

### View Service:
kubectl get service

### Show in browser:
minikube service hello-node

#### Scale Up/Down
kubectl scale deployments/hello-node --replicas=10

### Delete Service and Deployment
kubectl delete service hello-node
kubectl delete deployment hello-node

Reference:

* https://kubernetes.io/docs/tutorials/hello-minikube/
* https://medium.com/@brianbmathews/getting-started-with-minikube-docker-container-images-for-testing-kubernetes-locally-on-mac-e39adb60bd41
 



