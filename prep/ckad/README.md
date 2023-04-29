[CKAD](https://www.cncf.io/certification/ckad/) performance exam.

[Candidate Handbook](https://docs.linuxfoundation.org/tc-docs/certification/lf-handbook2)

[System Instructions](https://docs.linuxfoundation.org/tc-docs/certification/tips-cka-and-ckad)

# Core Concepts

`Node` - physical machine(server), where Kubernetes installed.

`Cluster` - List of Nodes.

`Kubernetes Master` - Node, that manages the Cluster.

`etcd` - distributed K-V store where.

`Kubelet` - Agent that runs on the node for providing health information about node to the master.

`Container Runtime` - underlining software that runs containers, e.g. Docker, CRI-O, rkt, etc.

`Kube API Server` - Installed on Master Node.

Information between Master(`kube-api-server`) and Worker Node(`kubelet`) is stored on Master `etcd`.

Master, Also has `controller` and `scheduler`.

## `kubectl` CLI for deployment and management

Check information about cluster:

```shell
kubectl cluster-info
```

Get all the nodes:

```shell
kubectl get nodes
```

## Container Runtime Interface(CRI)

Open Container Initiative(OCI)

- imagespec
- runtimespec
  <br>  
  Docker works without CRI

ContainerD is a CRI-compatible runtime.

Docker(itself) support was removed in `v1.24` of Kubernetes.
Now it works via ContainerD.

| `ctr`      | `crictl`       | `nerdctl`       
|------------|----------------|-----------------
| Debugging  | Debugging      | General Purpose 
| ContainerD | CRI compatible | ContainerD      

## Pods

`Pod` - smallest object, that you can create in Kubernetes.

`kubectl run` deploys docker container by creating Pod:

```shell
kubectl run nginx --image nginx
```

Get pods:

```shell
kubectl get pods
```

Creating Pod in YAML:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
  labels:
    app: myapp
    type: backend-utils
spec:
  containers:
    - name: nginx-container
      image: nginx
```

```shell
kubectl create -f pod-def.yml
```

Get Pods:

```shell
kubectl get pods
```

Describe Pod:

```shell
kubectl describe pod myapp-pod
```

```shell
kubectl run redis --image=redis123 --dry-run=client -o yaml > redis.yaml
```