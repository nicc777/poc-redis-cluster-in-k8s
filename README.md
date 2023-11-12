# poc-redis-cluster-in-k8s

A small experimental setup to test Redis cluster in Kubernetes [based on the guide](https://www.airplane.dev/blog/deploy-redis-cluster-on-kubernetes) from [Bharathiraja Shanmugam](https://github.com/bharathirajatut).

Tested on a local running Ubuntu 22.04 system using [this script](https://gist.github.com/nicc777/0f620c9eb2958f58173224f29b23a2ff) to deploy a small 4x node K3s Kubernetes cluster.

> **Warning**
> This is NOT intended for production deployments, but merely as a stepping stone to understand the deployment and usage of a Redis cluster in Kubernetes. Certain items are known not to be secure, for example the way the passwords are set in the Redis configuration ConfigMap.


