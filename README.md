# Kubernetes
Tutorials

Multi Host Container Scheduling :- kube-scheduler

Assigns pods to nodes at runtime 

Checks resources , quality of service and user specifications

Scalability :- Can support 5000 nodes clusters and 150000 pods

Persistent Storage for PODS

TCP HTTP or container execution health checks

Node health checks

Kubernetes is governed by Cloud Native Computing Foundation

KubeCon :- linuxfoundation (" Kubernetes Conf ")

slack :- https://kubernetes.slack.com

Companies providing container orchestration today are :
Kubernetes , Rancher , Docker Swarm , Mesos

Master Node is reponsible for managing kubernetes clusters
Kube API server allows you to interact with kubernetes API
Scheduler designs the pods to run on the specific node
Controller manager runs controller on master node

etcd is where all the cluster data is stored
kubectl is used to handle master node
kubectl has kubeconfig file with information which has server information and authentication info

Communication by the worker node is handle by kubelet process 
Commands :-    kubectl ( Master Node) ----- kubelet ( Communication between master node and worker node )

Node : Node serves as a worker machine in k8 cluster. Node can be physical computer or  a virtual machine
Node contains PODS which have multiple docker containers inside a single pod

Node must have following requ:
1. A kubelet running 
2. Container tooling like docker
3. A kube-proxy
4. Supervisord

POD is the simplest unit that you can interact with. You can create deploy or delete pods and its represents one running process on your cluster

POD must have following requ:

1. Your Docker application container
2. Storage resources
3. Unique network IP
4. Options that govern how the containers should run

POD states:

1. Pending ( POD is been created but containers are not running )
2. Running ( Atleast one of all containers are running in the POD )
3. Succeeded ( Means all the containers are running in the POD )
4. Failed ( One container in the POD has failed )
5. CrashLoopBackOff ( POD fails and kubernetes tries again and again to up the POD ) 


Benifits of Controllers :
1. Application Reliability 
2. Scaling
3. Load Balancing

Kinds of Controllers
1.ReplicaSets
2.Deployments
3.DaemonSets
4.Jobs
5.Services

ReplicaSets ( Ensures that a specific number of replicas for pods are running at all times )
Deployments ( A deployment controller provides declarative updates for pods and replica sets )
POD Management : Deployments running a specific replica sets allows us to deploy a number of pods and check their status 
of single unit , Scaling the pods too.


Pause and Resume in Deployment Controller ( Deployments ) 
Used with larger changesets
Pause deployment make changes resume deployment

DeamonSets : Ensures that all nodes run a copy of a specific POD


Service : Allows the communication betweeen one set of deployments with another

labels are key/value pairs that are attached to objects like pods, services and deployments.
***Labels are for users of kubernetes to identify attributes for objects



Example Labels : "release" , "stable", "release":"canary" 
"environment" : "dev" , "qa" , "production"


Kubelet Roles :
1. Communication with API server to see if pods have been assigned to nodes
2. Executes pod containers via a container engine
3. Mounts and runs the pod volume and secrets
4. Execute health checks to identify pod node status

***Podspecs : YAML file that describes a pod
kubelet takes the podspecs that are provided by the kube-apiserver and ensures that the containers are running according
to the podspecs



Three modes of kube-proxy
1.User space mode
2. IPtables mode 
3. Ipvs mode



Start : 

1.  https://kubernetes.io/docs/tasks/tools/install-kubectl/ ( install kubectl )
2. install minikube
3. (Takes docker) minikube start --driver=none
4. minikube start 
5. It will start all the docker containers
6. docker ps will show all the containers initiated by minikube start
7. kubectl get nodes (it will get u all the nodes on machine name, age , status , roles , version)
8. kubectl run hazelcast --image=hazelcast/hazelcast --port=5701
9. kubectl get deployments / pods
10. kubectl get pods -o wide
11. kubectl get rc,services
output:
NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
service/kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   2d2h

12. kubectl expose pod hazelcast --type=NodePort
13. kubectl get services
output
NAME         TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
hazelcast    NodePort    10.102.239.129   <none>        5701:30055/TCP   27s
kubernetes   ClusterIP   10.96.0.1        <none>        443/TCP          2d2h

14. minikube service hazelcas
output
|-----------|-----------|-------------|----------------------------|
| NAMESPACE |   NAME    | TARGET PORT |            URL             |
|-----------|-----------|-------------|----------------------------|
| default   | hazelcast |        5701 | http://192.168.2.107:30055 |
|-----------|-----------|-------------|----------------------------|


15. kubectl get all

output:
NAME            READY   STATUS    RESTARTS   AGE
pod/hazelcast   1/1     Running   0          13m

NAME                 TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
service/hazelcast    NodePort    10.102.239.129   <none>        5701:30055/TCP   5m43s
service/kubernetes   ClusterIP   10.96.0.1        <none>        443/TCP          2d2h

16. kubectl get pod/hazelcast -o yaml > kube.yml ( write into a yml file)
17.kubectl get rs -A

  # Scale a replicaset named 'foo' to 3.
  kubectl scale --replicas=3 rs/foo
  
  # Scale a resource identified by type and name specified in "foo.yaml" to 3.
  kubectl scale --replicas=3 -f foo.yaml
  
  # If the deployment named mysql's current size is 2, scale mysql to 3.
  kubectl scale --current-replicas=2 --replicas=3 deployment/mysql
  
  # Scale multiple replication controllers.
  kubectl scale --replicas=5 rc/foo rc/bar rc/baz
  
  # Scale statefulset named 'web' to 3.
  kubectl scale --replicas=3 statefulset/web

![Image description](https://drive.google.com/file/d/1BeAtFqwGTLCJMKKmYkgCntBLCIWCSoSM/view?usp=sharing)























