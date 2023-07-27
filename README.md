# kubernetes depl configuration


###  Starts a local Kubernetes cluster
if computer doesn't have VT-X/AMD-v enabled or Enabling it in the BIOS dosen't work add `--no-vtx-check`

```
minikube start --no-vtx-check --cpus='4' --memory='4000mb'
```

