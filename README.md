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

PS1> docker build --no-cache -f Dockerfile -t "hello-kubernetes:1.0" app
