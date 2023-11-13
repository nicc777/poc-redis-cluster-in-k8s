# Kubernetes Manifests

Here are the Kubernetes manifests used to deploy and test the Redis cluster.

There are two main files:

* [redis-lab01.yaml](./redis-lab01.yaml) - contains the Redis deployment all combined into a single file, as used in the first experiment.
* [client.yaml](./client.yaml) - contains a [Python Redis client](../test-service/README.md) to interact with the Redis cluster.


