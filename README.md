# argocd-demo
Demo install of ArgoCD.

```
# Install Kubernetes in Docker binary
go get -u sigs.k8s.io/kind

# Create the KinD kubernetes cluster
kind create cluster

# Make sure we're connecting to the right cluster
export KUBECONFIG="$(kind get kubeconfig-path --name="kind")"

# Create ArgoCD Namespace
kubectl create namespace argocd

# Install ArgoCD
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

# Open ArgoCD. Username admin, password is Argo server pod name
kubectl port-forward svc/argocd-server 8080:80 -n argocd

# Open ArgoCD in the browser
open http://localhost:8080

# Apply our new application
k apply -f argoapp.yaml -n argocd

# Port forward to the newly installed app
k port-forward svc/demo-argocd-demo 9090:80 -n default 

# Open the app in the browser
open http://localhost:9090
```