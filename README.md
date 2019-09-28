# Kubernetes Quick Reference Guide

## Common Commands

### Apply

How we make any changes to the kubernetes cluster

```bash
kubectl apply -f ./SIMPLEK8S/client-pod.yaml
```

### Get

See status of objects in kubernetes cluster

```bash
kubectl get pods
```

```bash
kubectl get services
```

### Describe

To get information about a object use describe

```bash
kubectl describe pods client-pod
```

## Object Types

- Pods: Runs one or more closely related containers

  - once created can only manually update the image

- Services: Sets up networking in a kubernetes Cluster

- Deployment: Maintains a set of identical pods ensuring that they have the correct config and that the right number exists

## Service Types

### NodePort

[NodePort documentation](https://kubernetes.io/docs/concepts/services-networking/service/#nodeport)

- port: The port other pods or other objects will use to access the service this points to

- tartgetPort: Port a pod is exposing internally

- nodePort: the port that you use to access pod inside your browser (outside access)
