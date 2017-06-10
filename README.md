# [Kubernetes](https://github.com/hrishikeshtak/Kubernetes-Running-Kubernetes-Locally-via-Minikube/blob/master/kubernetes.md) : Running-Kubernetes-Locally-via-Minikube

### Minikube starts a single node kubernetes cluster locally for purposes of development and testing.      
[Hello Minikube](https://kubernetes.io/docs/tutorials/stateless-application/hello-minikube/)

Minikube packages and configures a Linux VM, Docker and all Kubernetes components, optimized for local development. 

#### What Do We Need?

**1. VirtualBox:**          
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Download the latest version (> 5.0) of [VirtualBox](https://www.virtualbox.org/).

**2. Docker Toolbox:**     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;We will extensively use Docker Machine for the configuration. Download the stable version of [Docker Toolbox](https://www.docker.com/products/docker-toolbox).

**3. Installing minikube:**          
>\# curl -Lo minikube https://storage.googleapis.com/minikube/releases/v0.18.0/minikube-linux-amd64 && chmod +x minikube && sudo mv minikube /usr/local/bin/

**4. Install kubectl:**            
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;kubectl is a requirement for using minikube. kubectl command-line tool, which you can use to interact with Kubernetes clusters.         

>\# curl -Lo kubectl https://storage.googleapis.com/kubernetes-release/release/v1.6.0/bin/linux/amd64/kubectl && chmod +x kubectl && sudo mv kubectl /usr/local/bin/

**5. Starting the cluster:**             
We can run minikube command using either kvm or VirtualBox.        
To start a cluster, run minikube with Virtualbox driver:
>\# minikube start --vm-driver="virtualbox"         
Sarting local Kubernetes cluster...        
Starting VM...        
Downloading Minikube ISO         
 89.51 MB / 89.51 MB [==============================================] 100.00% 0s      
SSH-ing files into VM...         
Setting up certs...          
Starting cluster components...        
Connecting to cluster...       
Setting up kubeconfig...        
Kubectl is now configured to use the cluster.   
    
**Check the status of Minikube:**

>\# minikube status

**Check if kubectl is correctly configured:**

>\# kubectl get componentstatuses            
**NAME&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;STATUS&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MESSAGE&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ERROR**         
scheduler&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Healthy&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ok                   
controller-manager&nbsp;&nbsp;Healthy&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ok                   
etcd-0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Healthy&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{"health": "true"}         
 
If Everything success, then we installed minikube successfully.         
Now we deploy simple Hello-World Program using Docker

## Hello-World Program 
**Deploy and Run in Kubernetes**         

Point the Docker CLI to minikube:      

>\# eval $(minikube docker-env)

Later, when we no longer wish to use the Minikube host, we can undo this change by running:

>\# eval $(minikube docker-env -u)

#### Creating Node.js application     
Find server.js code in **hello-node/server.js**         
#### Creating a Docker container image      
Dockerfile is available in **hello-node/Dockerfile**

>\# cd hello-node/           
>\# docker build -f Dockerfile -t hello-node:v1 .          
\# docker images          

#### Creating a Deployment      
A Kubernetes Pod is a group of one or more Containers, tied together for the purposes of administration and networking. The Pod in this tutorial has only one Container. A Kubernetes Deployment checks on the health of our Pod and restarts the Pod's Container if it terminates.        

Use the kubectl run command to create a Deployment that manages a Pod.        
The Pod runs a Container based on our hello-node:v1 Docker image:

> **[kubernetes-basics](https://kubernetes.io/docs/tutorials/kubernetes-basics/explore-intro/)**           

>\# kubectl run hello-node --image=hello-node:v1 --port=8080          
deployment "hello-node" created            
 
> To view the Deployment:           
>\# kubectl get deployments        

> To view the Pod:           
>\# kubectl get pods

> To view cluster events:           
>\# kubectl get events       

> **[Creating a Service](https://kubernetes.io/docs/tutorials/kubernetes-basics/expose-intro/)**          

> By default, the Pod is only accessible by its internal IP address within the Kubernetes cluster.      
To make the hello-node Container accessible from outside the Kubernetes virtual network, we have to expose the Pod as a Kubernetes Service.

> \# kubectl expose deployment hello-node --type=LoadBalancer        
service "hello-node" exposed

>To view the Service we just created:           
> \# kubectl get services

> On Minikube, the LoadBalancer type makes the Service accessible through the minikube service command:

> \# minikube service hello-node          
Opening kubernetes service default/hello-node in default browser...



**OR you can create yaml conf file to deploy applications**    
Find conf files in **hello-node** directory 
     
>\# kubectl create -f hello-node-pod.yml             
pod "hello-node" created   
      
>\#kubectl get pods         
      
>\# kubectl create -f hello-node-svc.yml               
service "hello-node" created         

>\# kubectl get services  

>**To go inside pod & run bosh command**         
>\# kubectl exec -it \<pod_name\> /bin/bash


## Replication-Controller
Scale pods with replication-controller       
 
> \# kubectl create -f hello-node-rc.yml          
> \# kubectl get rc         
> To scale pods          
> \# kubectl scale rc hello-node --replicas 5        


## Cleaning up

Now we can clean up the resources we created in our cluster:

> \# kubectl delete service hello-node         
service "hello-node" deleted

> \# kubectl delete deployment hello-node          
deployment "hello-node" deleted

>To shut the cluster down, type "minikube stop":

> \# minikube stop           
Stopping local Kubernetes cluster...
Machine stopped.





