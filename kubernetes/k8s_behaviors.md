# Kubernetes behaviors: what if ...?


## What if a kubeconfig file is changed when it is being used by a component (e.g. kube-scheduler)?
* Very likelike the component won't be affected before it's restarted.
* This is because the kubeconfig was loaded on app startup, and saved in-memory in a struct.
* See [go-client code](https://github.com/kubernetes/client-go/blob/8f8241f9ef2dc939ecaf3cbdc80f6eb58227efd9/tools/clientcmd/client_config.go).