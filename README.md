# Kubernetes Quick Reference Guide

## Common Commands

### Deploy new files to cluster

```bash
kubectl apply -f client-pod.yaml
```

### See status of objects in kubernetes cluster

```bash
kubectl get pods
```

```bash
kubectl get services
```

## Service Types

### NodePort

[NodePort documentation](https://kubernetes.io/docs/concepts/services-networking/service/#nodeport)

- port: The port other pods or other objects will use to access the service this points to

- tartgetPort: Port a pod is exposing internally

- nodePort: the port that you use to access pod inside your browser (outside access)
