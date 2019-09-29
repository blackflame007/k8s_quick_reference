# Kubernetes Quick Reference Guide

## Common Commands

### Apply

How we make any changes to the kubernetes cluster
To create or update an object you must pass in the config file

```bash
kubectl apply -f ./SIMPLEK8S/client-pod.yaml
```

### Get

See status of objects in kubernetes cluster

```bash
kubectl get services
```

```bash
kubectl get deployments
```

```bash
kubectl get pods
```

### Describe

To get information about a object use describe

```bash
kubectl describe pods client-pod
```

### Delete

To delete an object you must pass in the config file that was used to create that object

```bash
kubectl delete -f ./SIMPLEK8S/client-pod.yaml
```

## Object Types

- <b>Services</b>: Sets up networking in a kubernetes Cluster

- <b>Deployment</b>: Replaces pod... Maintains a set of identical pods ensuring that they have the correct config and that the right number exists

  - Runs a set of identical pods (one or more)

  - Monitors the state of each pod, updates as necessary

  - Good for dev

  - Good for production

- <b>Pods</b>: Runs one or more closely related containers

  - once created can only manually update the image

  - Runs a single set of containers

  - Good for one-off dev purposes

  - Rarely used directly in production

## Service Types

### NodePort

[NodePort documentation](https://kubernetes.io/docs/concepts/services-networking/service/#nodeport)

- port: The port other pods or other objects will use to access the service this points to

- tartgetPort: Port a pod is exposing internally

- nodePort: the port that you use to access pod inside your browser (outside access)
