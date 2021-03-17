## Whath is Kubernates

Kubernetes is a portable, extensible, open-source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation. It has a large, rapidly growing ecosystem. Kubernetes services, support, and tools are widely available.

The name Kubernetes originates from Greek, meaning helmsman or pilot. Google open-sourced the Kubernetes project in 2014. Kubernetes combines over 15 years of Google's experience running production workloads at scale with best-of-breed ideas and practices from the community.


### Going back in time

![alt text](/doc/img/container_evolution.svg)

**Traditional deployment era:** Early on, organizations ran applications on physical servers. There was no way to define resource boundaries for applications in a physical server, and this caused resource allocation issues. For example, if multiple applications run on a physical server, there can be instances where one application would take up most of the resources, and as a result, the other applications would underperform. A solution for this would be to run each application on a different physical server. But this did not scale as resources were underutilized, and it was expensive for organizations to maintain many physical servers.

**Virtualized deployment era:** As a solution, virtualization was introduced. It allows you to run multiple Virtual Machines (VMs) on a single physical server's CPU. Virtualization allows applications to be isolated between VMs and provides a level of security as the information of one application cannot be freely accessed by another application.

Virtualization allows better utilization of resources in a physical server and allows better scalability because an application can be added or updated easily, reduces hardware costs, and much more. With virtualization you can present a set of physical resources as a cluster of disposable virtual machines.

**Container deployment era:** Containers are similar to VMs, but they have relaxed isolation properties to share the Operating System (OS) among the applications. Therefore, containers are considered lightweight. Similar to a VM, a container has its own filesystem, share of CPU, memory, process space, and more. As they are decoupled from the underlying infrastructure, they are portable across clouds and OS distributions.

Containers have become popular because they provide extra benefits, such as:

- Agile application creation and deployment
- Continuous development, integration, and deployment
- Observability not only surfaces OS-level information and metrics, but also application health and other signals.
- Environmental consistency across development, testing, and production: Runs the same on a laptop as it does in the cloud.
- Cloud and OS distribution portability: Runs on Ubuntu, RHEL, CoreOS, on-premises, on major public clouds, and anywhere else.
- Loosely coupled, distributed, elastic, liberated micro-services: applications are broken into smaller, independent pieces and can be deployed and managed dynamically.
- Resource isolation: predictable application performance.
- Resource utilization: high efficiency and density.


### Why you need Kubernetes and what it can do 

Containers are a good way to bundle and run your applications. In a production environment, you need to manage the containers that run the applications and ensure that there is no downtime. For example, if a container goes down, another container needs to start. Wouldn't it be easier if this behavior was handled by a system?

That's how Kubernetes comes to the rescue! Kubernetes provides you with a framework to run distributed systems resiliently. It takes care of scaling and failover for your application, provides deployment patterns, and more. For example, Kubernetes can easily manage a canary deployment for your system.

Kubernetes provides you with:

- Service discovery and load balancing
- Storage orchestration
- Automated rollouts and rollbacks
- Self-healing
- Secret and configuration management

### What Kubernetes is not

Kubernetes is not a traditional, all-inclusive PaaS (Platform as a Service) system. Since Kubernetes operates at the container level rather than at the hardware level, it provides some generally applicable features common to PaaS offerings, such as deployment, scaling, load balancing, and lets users integrate their logging, monitoring, and alerting solutions. However, Kubernetes is not monolithic, and these default solutions are optional and pluggable. Kubernetes provides the building blocks for building developer platforms, but preserves user choice and flexibility where it is important.

Kubernetes:

- Does not limit the types of applications supported. Kubernetes aims to support an extremely diverse variety of workloads, including stateless, stateful, and data-processing workloads. If an application can run in a container, it should run great on Kubernetes.
- Does not deploy source code and does not build your application. Continuous Integration, Delivery, and Deployment (CI/CD) workflows are determined by organization cultures and preferences as well as technical requirements.
- Does not provide application-level services, such as middleware (for example, message buses), data-processing frameworks (for example, Spark), databases (for example, MySQL), caches, nor cluster storage systems (for example, Ceph) as built-in services.
- Does not dictate logging, monitoring, or alerting solutions. It provides some integrations as proof of concept, and mechanisms to collect and export metrics.
- Does not provide nor mandate a configuration language/system (for example, Jsonnet).
- Does not provide nor adopt any comprehensive machine configuration, maintenance, management, or self-healing systems.
Additionally, Kubernetes is not a mere orchestration system. In fact, it eliminates the need for orchestration. The technical definition of orchestration is execution of a defined workflow: first do A, then B, then C. In contrast, Kubernetes comprises a set of independent, composable control processes that continuously drive the current state towards the provided desired state. It shouldn't matter how you get from A to C. Centralized control is also not required. This results in a system that is easier to use and more powerful, robust, resilient, and extensible.

### Kubernates resources

- **Cluster:**
- - **Master:** Gerencia o cluster, manter e atualizar o estado desejado, receber e executar comandos
- - - **api:** receber e executar novos comandos
- - - **c-m:** (controller manager) manter e atualizar o estado desejado
- - - **sched:** define onde determinado pod vai ser executado no cluster
- - - **etcd:** armazena todos os dados vitais do cluster atraves de um banco chave-valor
- - **Node:** Executar as aplicações
- - - **Kubelet:** execução dos pods dentro dos nodes
- - - **K-proxy:** responsavel pela comunicação entre os nodes dentro do cluster


#### Pods 

Pods are the smallest deployable units of computing that you can create and manage in Kubernetes.

A Pod (as in a pod of whales or pea pod) is a group of one or more containers, with shared storage and network resources, and a specification for how to run the containers. A Pod's contents are always co-located and co-scheduled, and run in a shared context. A Pod models an application-specific "logical host": it contains one or more application containers which are relatively tightly coupled. In non-cloud contexts, applications executed on the same physical or virtual machine are analogous to cloud applications executed on the same logical host.


> In terms of Docker concepts, a Pod is similar to a group of Docker containers with shared namespaces and shared filesystem volumes.


![alt text](/doc/img/pod.svg)

![alt text](/doc/img/module_03_nodes.svg)

The applications in a pod don't must be have the same port.


#### API

A API além de receber comandos do mundo esterno é responsavel por fazer a comunicação com os componentes do Master e também com os nodes.

Através da api podemos criar pods, editar um replica set, ler os dados de um deployment, deletar um  volume.

Para realizar a comucação com a api é utilizado o kubeclt.


### minikube

minikube is local Kubernetes, focusing on making it easy to learn and develop for Kubernetes.

All you need is Docker (or similarly compatible) container or a Virtual Machine environment, and Kubernetes is a single command away: minikube start

Link to [configure kvm2](https://minikube.sigs.k8s.io/docs/drivers/kvm2/) 

```
$ minikube start

------- result ---------

😄  minikube v1.18.1 on Ubuntu 18.04
❗  Both driver=kvm2 and vm-driver=kvm2 have been set.

    Since vm-driver is deprecated, minikube will default to driver=kvm2.

    If vm-driver is set in the global config, please run "minikube config unset vm-driver" to resolve this warning.
			
✨  Using the kvm2 driver based on user configuration
👍  Starting control plane node minikube in cluster minikube
🔥  Creating kvm2 VM (CPUs=2, Memory=3900MB, Disk=20000MB) ...
🐳  Preparing Kubernetes v1.20.2 on Docker 20.10.3 ...
    ▪ Generating certificates and keys ...
    ▪ Booting up control plane ...
    ▪ Configuring RBAC rules ...
🔎  Verifying Kubernetes components...
    ▪ Using image gcr.io/k8s-minikube/storage-provisioner:v4
🌟  Enabled addons: storage-provisioner, default-storageclass
🏄  Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default
```

### kubectl

> The Kubernetes command-line tool, kubectl, allows you to run commands against Kubernetes clusters. You can use kubectl to deploy applications, inspect and manage cluster resources, and view logs.

#### Commands

**Pods**

```
# list nodes
$ kubectl get nodes

# create a pod whith nginx image and name nginx-pod
$ kubectl run nginx-pod --image=nginx

# list pods
$ kubectl get pods

# list pods and watch de logs
$ kubectl get pods --watch

# get info of created pod
$ kubectl describe pod nginx-pod

# Is possible edit pod configurations
$  kubectl edit pod nginx-pod

# delete pod
$ kubectl delete pod nginx-pod
```

For create pods in declataive file uses the .yaml file with configurations and run de command: 

File: `v1-pods/primeiro-pod.yaml`

```
# create pod
$ kubectl apply -f primeiro-pod.yaml 

# delete pod
$ kubectl delete -f primeiro-pod.yaml

# run interative bash of pod
$ kubectl exec -it primeiro-pod -- bash

# get de cluster IP ( use the INTERNAL-IP:EXPOSED_PORT_OF_NODE_PORT_SERVICE))
$ kubectl get nodes -o wide
```