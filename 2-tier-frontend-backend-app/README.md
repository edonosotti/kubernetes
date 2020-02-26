# 2-tier frontend+backend Sinatra app

![AWS](aws.jpg)

The `YAML` files in this directory will deploy a simple 2-tier
(`frontend` + `backend`) `Sinatra` (`Ruby`) application, wrapped
into a `Docker` image to a `Kubernetes` cluster.

This configuration was created during an **AWS Engineering Learning
Series session on EKS**, but it will run on any standard `Kubernetes`
cluster able to provision the required resources. It is a good starting
point to learn about the technologies listed above.

In particular, this 2-tier setup shows how to expose the `frontend`
application to the _public_ network (but with **limited access to a
single IP address**) and the `backend` service to the _private_
network, so that it is isolated from the outside world.

The [`Docker` image](https://hub.docker.com/repository/docker/edonosotti/aws-eks-training-frontend)
for the `frontend` application was built on a `base` image provided
by `AWS`. See the `Docker Hub` page for details.
The `backend` uses a common image provided by `AWS`.


## Prerequisites

 1. A working [`Kubernetes`](https://kubernetes.io) cluster or a
    compatible host, such as:
    * [`Minikube`](https://kubernetes.io/docs/setup/learning-environment/minikube/)
    * [`MicroK8s`](https://microk8s.io)
 2. [`kubectl`](https://kubernetes.io/docs/tasks/tools/install-kubectl/) with
    a valid set of credentials to grant admin access to the `k8s` cluster

## Usage

Edit the [`frontend_service.yml`](frontend_service.yml) file and change
(or remove) the `spec/loadBalancerSourceRanges` to allow access from your
IP address (or make it available to the public).

Run:

```
$ kubectl apply -f backend_deployment.yml
$ kubectl apply -f backend_service.yml
$ kubectl apply -f frontend_deployment.yml
$ kubectl apply -f frontend_service.yml
```


## Further reading

See the links below for details on the project and the application:

 * https://github.com/aws-els-cpt/eks/blob/master/project/README.md
 * https://github.com/aws-els-cpt/eks
 * https://github.com/aws-els-lin/eks
