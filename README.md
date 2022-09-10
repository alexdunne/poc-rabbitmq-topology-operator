# poc-rabbitmq-topology-operator

Proof of concept (PoC) showing Kubernetes (K8s) RabbitMQ (RMQ) Topology Operator in action

## Getting Started

- Set up [Kind](https://kind.sigs.k8s.io/) to run a K8s cluster locally
- Set up [RMQ Cluster Operator](https://www.rabbitmq.com/kubernetes/operator/install-operator.html)
- Set up [RMQ Topology Operator](https://github.com/rabbitmq/messaging-topology-operator/#quickstart)

## Running PoC

- k kustomize ./cluster | kubectl apply -f -
- k kustomize ./rabbit | kubectl apply -f -

## Notes

- Manually deleting a resource via the RMQ Admin UI did not cause the Operator to reconcile. Reconcile loop can be triggered by updating a resource (i.e. update a label) or by setting the [SYNC_PERIOD](https://github.com/rabbitmq/messaging-topology-operator/pull/369) environment variable to determine how often resources should be double-checked for drift from the desired state.
- Renaming K8s resources caused existing resources to not be cleaned up. Could be intentional to allow a transition period.
- Policies are super easy to work with as a K8s resources