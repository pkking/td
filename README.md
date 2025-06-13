## Intro
A demo for setting up a pipline using [tekton](https://tekton.dev/) and integrated with github webhook

## Quick start

### setup KIND
```bash
go install sigs.k8s.io/kind@v0.29.0
kind create cluster --name tekton-kind

```
### setup tekton

install tekton through [tekton operator](https://github.com/tektoncd/operator/blob/main/docs/install.md)
```bash
 kubectl apply -f https://storage.googleapis.com/tekton-releases/operator/latest/release.yaml
```

### setup network
setup the network using [cloud-provider-kind](https://github.com/kubernetes-sigs/cloud-provider-kind), so that we can access service in [KIND](https://github.com/kubernetes-sigs/kind)
```bash
go install sigs.k8s.io/cloud-provider-kind@latest 
cloud-provider-kind # run cloud-provider-kind as a foreground process
```

### apply our tekton deployment
```bash
kubectl apply -f deploy/trigger.yaml # trigger, serviceaccount
kubectl apply -f deploy/pipeline.yaml # pipeline called by trigger
kubectl apply -f deploy/task.yaml # task called by pipeline
```