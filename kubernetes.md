# Kubernetes or K8s

#### Kubernetes is an open source container orchestration tool designed to automate deploying, scaling, and operating containerized applications
[kubernetes-basics](https://kubernetes.io/docs/tutorials/kubernetes-basics/)
#### Kubernetes Terminology

**1.Nodes:**        
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Hosts that run Kubernetes applications.
    
**2.Containers:**           
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Units of packaging.

**3.Pods:**         
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Units of deployment that can be scheduled and managed.          
Its a logical collection of containers that belong to an application. A pod consists of one or more containers, and they are guaranteed to be co-located on the host machine and can share resources. 
Each pod in Kubernetes is assigned a unique (within the cluster) IP address.
   
**4.Replication Controller:**           
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Ensures availability and scalability. It handles replication and scaling by running a specified number of copies of a pod across the cluster.
It also handles creating replacement pods if the underlying node fails.

**5.Labels:**          
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Identification Key-value pairs for API object such as pods and nodes.
    
**6.Selectors:**       
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Like labels, selectors are the primary grouping mechanism in Kubernetes, and are used to determine the components to which an operation applies.

**7.Services:**        
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Collection of pods that work together, and exposed as an endpoint.
