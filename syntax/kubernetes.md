<!-- TOC -->

- [Pods](#pods)
  - [Create](#create)
  - [From Private Registry](#from-private-registry)
  - [Init Container](#init-container)
  - [Lifecycle Hooks](#lifecycle-hooks)
    - [PostStart](#poststart)
    - [PreStop](#prestop)
- [Deployment](#deployment)
  - [Rolling](#rolling)
    - [Upgrade](#upgrade)
    - [Downgrade](#downgrade)
    - [History](#history)
    - [Pause/Resume](#pauseresume)
- [ConfigMap](#configmap)
  - [Create](#create-1)
  - [Edit](#edit)
  - [Usage](#usage)
    - [Single Var](#single-var)
    - [Whole ConfigMap](#whole-configmap)
    - [Files with Volume](#files-with-volume)
- [Secrets](#secrets)
  - [Create](#create-2)
  - [Reading as Volume](#reading-as-volume)
  - [Reading as Env](#reading-as-env)
- [ServiceAccount](#serviceaccount)
  - [Create](#create-3)
- [AutoScaling](#autoscaling)
  - [HorizontalPodAutoscaler](#horizontalpodautoscaler)
- [Kubectl Config](#kubectl-config)
  - [Cluster](#cluster)
    - [Create](#create-4)
    - [Modify Credentials](#modify-credentials)
  - [Context](#context)
    - [Create/Update](#createupdate)
    - [Switch](#switch)

<!-- /TOC -->
## Pods
### Create
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: kubia
spec:
  serviceAccountName: account-name
  containers:
  - name: server
    image: nginx
    resources:
      requests:
        cpu: 20m
        memory: 200M
      limits:
        cpu: 100m
        memory: 1G
```
### From Private Registry
```sh
kubectl create secret docker-registry <name> \
  --docker-username=username \
  --docker-password=password \
  --docker-email=email@docker.com
```
```yaml
spec:
  imagePullSecrets:
  - name: my-secret
```

### Init Container
```yaml
spec:
  initContainers:
  - name: init
    image: busybox
    command: ["/bin/sh", "-c"]
```

### Lifecycle Hooks
#### PostStart
```yaml
spec:
  containers:
  - ...
    lifecycle:
      postStart:
        exec:
          command: ["/bin/sh", "-c"]
```

#### PreStop
```yaml
spec:
  containers:
  - ...
    lifecycle:
      preStop:
        exec:
          command: ["/bin/sh", "-c"]
```

## Deployment
> Use --record on creation of a Deployment
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: kubia
spec:
  replicas: 3
  minReadySeconds: 10
  strategy:
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 0
    type: RollingUpdate
  selector:
    matchLabels:
      app: kubia
  template:
    # ...PodTemplate
```

### Rolling

#### Upgrade
```sh
kubectl set image deployment <name> <container_name>=<image_name>
kubectl edit deployment <name>
```
#### Downgrade
```sh
kubectl rollout undo deplyment <name>
kubectl rollout undo deplyment <name> --to-revision=n
```

#### History
```sh
kubectl rollout history deployment <name>
```
#### Pause/Resume
```sh
kubectl rollout pause deployment <name>
kubectl rollout resume deployment <name>
```

## ConfigMap
### Create
```sh
kubectl create configmap <name> --from-literal=sleep-interval=25
kubectl create configmap <name> --from-tile=config-file.conf
kubectl create configmap <name> --from-file=dir/
```

### Edit
```sh
kubectl edit configmap <name>
```

### Usage
#### Single Var
```yaml
kind: Pod
spec:
  containers:
  - ...
    env:
    - name: API_URL
      valueFrom:
        configMapKeyRef:
          name: my-config-map
          key: my-key
```

#### Whole ConfigMap
```yaml
kind: Pod
spec:
  containers:
  - ...
    envFrom:
    - prefix: CONFIG_
      configMapRef:
        namme: my-config-map
```
#### Files with Volume
```yaml
kind: Pod
spec:
  containers:
  - ...
    volumeMounts:
    - name: my-volume
      mountPath: /etc/conf.d
      readOnly: true
  volumes:
  - name: my-volume
    configMap:
      name: my-config-map
```

## Secrets
### Create
```sh
kubectl create secret generic <name> --from-file=ca.cert
```

### Reading as Volume
```yaml
kind: Pod
spec:
  containers:
  - ...
    volumeMounts:
    - name: my-volume
      mountPath: /etc/certs
      readOnly: true
  volumes:
  - name: my-volume
    secret:
      secretName: my-secret
```

### Reading as Env
```yaml
kind: Pod
spec:
  containers:
  - ...
    env:
    - name: FOO_SECRET
      valueFrom:
        secretKeyRef:
          name: my-secret
          key: key
```

## ServiceAccount
### Create
```sh
kubectl create serviceaccount <name>
```

```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: my-service-account
imagePullSecrets:
- name: my-registry-secret
```

## AutoScaling
### HorizontalPodAutoscaler
```sh
kubectl autoscale deployment <name> --cpu-percent=nn --min=n --max=n
```

## Kubectl Config
### Cluster
#### Create
```sh
kubectl config set-cluster <cluster-name> --server=<cluster-ip>
  --certificate-authority=<path> 
  --username=<username> --password=<password>
  --token=<token>
```
#### Modify Credentials
```sh
kubectl config set-credentials <cluster-name>
  --certificate-authority=<path> 
  --username=user --password=password
  --token=<token>
```

### Context
#### Create/Update
```sh
kubectl config set-context <context-name> --cluster=<cluster-name> --namespace=<namespace>
```

#### Switch
```sh
kubectl config use-context <context-name>
```