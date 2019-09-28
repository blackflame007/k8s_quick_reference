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
kubectl describe pods ./SIMPLEK8S/client-pod.yaml
```

## Service Types

### NodePort

[NodePort documentation](https://kubernetes.io/docs/concepts/services-networking/service/#nodeport)

- port: The port other pods or other objects will use to access the service this points to

- tartgetPort: Port a pod is exposing internally

- nodePort: the port that you use to access pod inside your browser (outside access)
