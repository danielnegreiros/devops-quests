# Local Setup

## Install microk8s

- Check if everything makes sense with your environment

```bash
sudo snap install microk8s --classic
mkdir -p ~/.kube
sudo usermod -a -G microk8s ${USER}
sudo chown -R ${USER} ~/.kube

# allow use host as storage for automatic pvc/pv creation and allocation
exit # reconnect
microk8s enable hostpath-storage
microk8s config > ~/.kube/config

# install tools - kubectl
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
echo 'source <(kubectl completion bash)' >>~/.bashrc

# install helm
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash

# k9s
wget https://github.com/derailed/k9s/releases/download/v0.50.9/k9s_Linux_amd64.tar.gz
tar -xvf k9s_Linux_amd64.tar.gz
sudo mv k9s /usr/local/bin/

# argocd cli
curl -sSL -o argocd-linux-amd64 https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd64
sudo install -m 555 argocd-linux-amd64 /usr/local/bin/argocd
rm argocd-linux-amd64


# If you like clean start
sudo reboot
```

## Install ArgoCD

```bash
cd devops-quests/deployment/argocd
helm dependency build
helm upgrade --install argo . -f ./values.yaml -n argo --create-namespace

# Check initial secret
kubectl get secret argocd-initial-admin-secret -n argo -o jsonpath='{.data.password}' | base64 -d; echo
```

## Install ArgoCD Applications

```bash
cd devops-quests/deployment/applications/apps-inventory
helm upgrade --install -n=argo argo-apps ./ -f ./values.yaml --create-namespace
```
