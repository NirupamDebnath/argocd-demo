# argocd-demo

1. kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath='{.data.password}' | base64 --decode
2. kubectl label namespace argocd istio-injection=enabled
3. kubectl apply -f argocd-gateway.yaml -n argocd

Install argocd cli

curl -sSL -o argocd-linux-amd64 https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd64
sudo install -m 555 argocd-linux-amd64 /usr/local/bin/argocd
rm argocd-linux-amd64

argocd login localhost:8080
argocd app list
argocd app create ms-elasticsearch --repo https://github.com/NirupamDebnath/argocd-demo.git --revision main --path efk-singlenode --dest-server https://kubernetes.default.svc --dest-namespace elasticsearch --sync-option createNamespace=true

1. kubectl port-forward svc/argocd-server -n argocd 8080:443
