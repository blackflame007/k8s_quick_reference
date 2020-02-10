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

### Create

To create an object without a config file we can use an imperative command to create a new object

```bash
kubectl create secret generic <secret_name> --from-literal key=value
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

  `--from-literal` is what allows us to store the secret information in this actual command using a key and value

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



### ClusterIP

[ClusterIP documentation](https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types)

### LoadBalancer

[LoadBalancer documentation](https://kubernetes.io/docs/concepts/services-networking/service/#loadbalancer)

### ExternalName

[ExternalName documentation](https://kubernetes.io/docs/concepts/services-networking/service/#externalname)

### [Nginx-Ingress](https://github.com/kubernetes/ingress-nginx/)

Read more about [nginx-ingress](https://www.joyfulbikeshedding.com/blog/2018-03-26-studying-the-kubernetes-ingress-system.html)

#### Install nginx-ingress for docker desktop (windows and mac)

1. Make sure you executed the mandatory generic script:

- ```bash
  kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/static/mandatory.yaml
  ```

2. Execute the provider specific script to enable the service:

- ```bash
  kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/static/provider/cloud-generic.yaml
  ```
  
 3. Verify the service was enabled by running the following:
 
- ```bash
  kubectl get svc -n ingress-nginx
  ```
#### Install nginx-ingress with helm

```bash
helm repo add stable https://kubernetes-charts.storage.googleapis.com/
```

```bash
helm install my-nginx stable/nginx-ingress --set rbac.create=true 
```
 ## Helm
 
 Helm is a package manager for kubernetes and allows you to install packages through repos called charts
 
 ### Install Helm 3
 
 Get the download binary
 ```bash
 curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3
 ```
 
 Change permissions to execute the downloaded file
 ```bash
 chmod 700 get_helm.sh
 ```
 
 Running the script should install helm 3
 
 ```bash
 ./get_helm.sh
 ```

 ## Cluster
 
 ### Setting up a new Cluster on Google Cloud Platform(GCP)
 
 Open googles built in shell and configure your gcloud to use your cluster
 
1. Configure your gcloud to use your google projects ID

- ```bash
    gcloud config set project multi-k8s-test-1234567
  ```

2. Configure your gcloud to use the zone your cluster is located

- ```bash
    gcloud config set compute/zone us-west1-a
  ```
  
3. Configure your gcloud to use the cluster you have made

- ```bash
    gcloud container clusters get-credentials multi-cluster-demo
  ```

