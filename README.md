# Kubernetes Quick Reference Guide

We are using a [declarative](https://tylermcginnis.com/imperative-vs-declarative-programming/) approach when using kubernetes

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

- **Services**: Sets up networking in a kubernetes Cluster

- **Deployment**: Replaces pod... Maintains a set of identical pods ensuring that they have the correct config and that the right number exists

  - Runs a set of identical pods (one or more)

  - Monitors the state of each pod, updates as necessary

  - Good for dev

  - Good for production

- **Pods**: Runs one or more closely related containers

  - once created can only manually update the image

  - Runs a single set of containers

  - Good for one-off dev purposes

  - Rarely used directly in production

- **Secrets**: Securely stores one or more pieces of information in the cluster such as a database password

  ```bash
  kubectl create secret generic <secret_name> --from-literal key=value
  ```

  - We want to create secrets in the cluster manually(take an imperative approach) to prevent this data from being exposed in plain text in our YAML files
  - Secret types

    - **generic**: [generic](https://kubernetes.io/docs/concepts/configuration/secret/) type indicates we are saving some arbitrary number of key value pairs together

    - **docker-registry**: [docker-registry](https://kubernetes.io/docs/concepts/containers/images/#specifying-imagepullsecrets-on-a-pod) type indicates Authentication with a custom container registry

    - **tls**: [tls](https://kubernetes.github.io/ingress-nginx/user-guide/tls/) .pem files and CA secret type

## Service Types

### NodePort

[NodePort documentation](https://kubernetes.io/docs/concepts/services-networking/service/#nodeport)

- port: The port other pods or other objects will use to access the service this points to

- tartgetPort: Port a pod is exposing internally

- nodePort: the port that you use to access pod inside your browser (outside access)
