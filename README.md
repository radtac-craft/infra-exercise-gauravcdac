### Prerequisites Install EKSCTL and Kubectl

## Refer this document to install kubectl
https://docs.aws.amazon.com/eks/latest/userguide/install-kubectl.html

```bash
$ curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
$ sudo mv /tmp/eksctl /usr/local/bin
```

### To create the cluster

## To configure AWS
```bash
$ aws configure
```

## To create a single node cluster
```bash
$eksctl create cluster -f cluster.yaml --write-kubeconfig --set-kubeconfig-context
```
### Standard Configuration

Deploy to your Kubernetes cluster using the hello-kubernetes.yaml, which contains definitions for the service and deployment objects:

```yaml
# hello-kubernetes.yaml
apiVersion: v1
kind: Service
metadata:
  name: hello-kubernetes
spec:
  type: LoadBalancer
  ports:
  - port: 80
    targetPort: 8080
  selector:
    app: hello-kubernetes
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-kubernetes
spec:
  replicas: 3
  selector:
    matchLabels:
      app: hello-kubernetes
  template:
    metadata:
      labels:
        app: hello-kubernetes
    spec:
      containers:
      - name: hello-kubernetes
        image: hello-kubernetes:1.0
        ports:
        - containerPort: 8080
```

```bash
$ kubectl apply -f yaml/hello-kubernetes.yaml
```

```bash
$ kubectl get service hello-kubernetes
```

## Build Container Image

```bash
$ docker build --no-cache -f Dockerfile -t "hello-kubernetes:1.0" app
```
