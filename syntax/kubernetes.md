<!-- TOC -->

- [Volumes](#volumes)
  - [StorageClass](#storageclass)
  - [PersistentVolume](#persistentvolume)
  - [PersistentVolumeClaim](#persistentvolumeclaim)
- [Pods](#pods)
  - [Create](#create)
- [Services](#services)
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
## Volumes
### StorageClass
[Docs](https://kubernetes.io/docs/concepts/storage/storage-classes/)
```yaml
kind: StorageClass
apiVersion: storage.k8s.io/v1
metadata:
  name: my-storage-class
provisioner: provisioner
reclaimPolicy: Retain|Delete
```

### PersistentVolume
```yaml
apiVersion: storage.k8s.io/v1
kind: PersistentVolume
metadata:
  name: pv
spec:
  capacity:
    storage: 5G
  volumeMode: Filesystem
  accessModes:
    - ReadWriteOnce
    - ReadOnlyMany
    - ReadWriteMany
  persistentVolumeReclaimPolicy: Retain|Delete
```

### PersistentVolumeClaim
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pvc
spec:
  accessModes:
    - ReadWriteOnce
    - ReadOnlyMany
    - ReadWriteMany
  volumeMode: Filesystem
  resources:
    requests:
      storage: 8G
  storageClassName: scn
```

<!-- END Volumes -->
## Pods
### Create
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: kubia
spec:
  serviceAccountName: account-name
  imagePullSecrets:
  - name: my-secret
  containers:
  - name: server
    image: nginx
    restartPolicy: Always|OnFailure|Never
    resources:
      requests:
        cpu: 20m
        memory: 200M
      limits:
        cpu: 100m
        memory: 1G
    volumeMounts:
    - name: volume
      mountPath: /var/data
    lifecycle:
      postStart:
        exec:
          command: ["/bin/sh", "-c"]
      preStop:
        exec:
          command: ["/bin/sh", "-c"]
    livenessProbe:
      httpGet:
        path: /heath
        port: 8080
        httpHeaders:
        - name: X-Custom-Header
          value: value
      initialDelaySeconds: 15
      timeoutSeconds: 1
    volumes:
    - name: volume
      persistentVolumeClaim:
        name: pvc
  initContainers:
  - name: init-container
    image: busybox
    command: ['sh', '-c']
```
```sh
kubectl create secret docker-registry <name> \
  --docker-username=<username> \
  --docker-password=<password> \
  --docker-email=<email> \
  --docker-server=<server>
```
<!-- END PODS -->

## Services
```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  ports:
  - protocol: TCP
    port: 80
    targetPort: 8080
```

<!-- END SERVICES -->

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

```yaml
apiVersion: v1
data:
  API_URL: "localhost"
metadata:
  name: my-config
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
    volumeMounts:
    - name: my-volume
      mountPath: /etc/conf.d
      readOnly: true
    env:
    - name: API_URL
      valueFrom:
        configMapKeyRef:
          name: my-config-map
          key: my-key
    envFrom:
    - prefix: CONFIG_
      configMapRef:
        namme: my-config-map
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