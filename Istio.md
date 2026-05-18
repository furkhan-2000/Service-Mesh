Istio bundles CRDs inside the control plane manifest

# Install Cli 
curl -L https://istio.io/downloadIstio | ISTIO_VERSION=1.23.0 sh -
cd istio-1.23.0


# Verify:
./bin/istioctl version

# If you want to run istioctl from any directory, then you can add it to PATH:
export PATH=$PWD/bin:$PATH

# Pre‑Check Cluster: 
./bin/istioctl x precheck

# Install Istio Control Plane
./bin/istioctl install --set profile=default -y

# Enable Sidecar Injection:   Namespace level
    kubectl label namespace myapp istio-injection=enabled
  # Deployment Level 
  metadata:
  annotations:
    sidecar.istio.io/inject: "true"

# Verify Mesh: 
./bin/istioctl proxy-status
