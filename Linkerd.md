CRDs → Control Plane → Sidecars


# Install CLI 

curl -sL https://run.linkerd.io/install | LINKERD2_VERSION=stable-2.14.10 sh

export PATH=$PATH:$HOME/.linkerd2/bin
echo 'export PATH=$PATH:$HOME/.linkerd2/bin' >> ~/.bashrc
source ~/.bashrc

Verify:
linkerd version


# Install Linkerd Control Plane (from Bastion)

linkerd check --pre

linkerd install --crds  | kubectl apply -f -      ~ install CRD's
linkerd install | kubectl apply -f -                 ~ install control plane
linkerd check

# Enable Sidecar Injection
Option A — Namespace level (recommended)
kubectl annotate namespace myapp linkerd.io/inject=enabled

Option B — Deployment level
Add inside YAML:
metadata:
  annotations:
    linkerd.io/inject: "enabled"

Redeploy the app.