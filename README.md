# poc-redis-cluster-in-k8s

A small experimental setup to test Redis cluster in Kubernetes, initially .

Tested on a local running Ubuntu 22.04 system using [this script](https://gist.github.com/nicc777/0f620c9eb2958f58173224f29b23a2ff) to deploy a small 4x node K3s Kubernetes cluster.

> **Warning**
> This is NOT intended for production deployments, but merely as a stepping stone to understand the deployment and usage of a Redis cluster in Kubernetes. Certain items are known not to be secure, for example the way the passwords are set in the Redis configuration ConfigMap.

# Lab Notes

## Round 1

|               | Notes                                                                                                                                                    |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| Objective     | Run the Redis HA Cluster in Kubernetes                                                                                                                   |
| Initial setup | [based on the guide](https://www.airplane.dev/blog/deploy-redis-cluster-on-kubernetes) from [Bharathiraja Shanmugam](https://github.com/bharathirajatut) |

_**Deployment:**_


Command:

```shell
kubectl apply -f kubernetes/redis-lab01.yaml
```

_**Findings:**_

Command 1:

```shell
kubectl get all -n poc
```

Output 1:

```text
NAME          READY   STATUS    RESTARTS   AGE
pod/redis-0   1/1     Running   0          85m
pod/redis-1   1/1     Running   0          84m
pod/redis-2   1/1     Running   0          84m
pod/redis-3   1/1     Running   0          84m
pod/redis-4   1/1     Running   0          83m

NAME            TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)    AGE
service/redis   ClusterIP   None         <none>        6379/TCP   85m

NAME                     READY   AGE
statefulset.apps/redis   5/5     85m
```

The cluster was UP, but this is only ONE master with a couple of slaves.

After some more reading and thinking about it, I decided to try a multi-master approach with sentinel.

Additional reading:

* ( :moneybag: paywall) [Setup Persistence Redis Cluster in Kubernetes](https://medium.com/zero-to/setup-persistence-redis-cluster-in-kubertenes-7d5b7ffdbd98)
* ( :date: old/outdated ) [Reliable, Scalable Redis on Kubernetes](https://github.com/kubernetes/examples/blob/master/staging/storage/redis/README.md)
* [Bitnami package for Redis(R) Cluster](https://github.com/bitnami/charts/tree/main/bitnami/redis-cluster)

The latter item in the reading list seems to be the next logic step in the experiment.

_**Cleanup:**_

```shell
kubectl delete -f kubernetes/redis-lab01.yaml
```