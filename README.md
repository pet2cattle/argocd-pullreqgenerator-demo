

k create ns argocd
helm repo add argo https://argoproj.github.io/argo-helm
helm install argocd argo/argo-cd -n argocd -f helpers/argocd_values.yaml




minikube addons enable registry

minikube addons enable ingress




minikube ssh cat /etc/hosts | grep registry.kube-system.svc.cluster.local >/dev/null 2>&1|| (kubectl get svc registry -n kube-system >/dev/null 2>&1 && minikube ssh echo "$(kubectl get svc registry -n kube-system -o jsonpath='{ .spec.clusterIP }') registry.kube-system.svc.cluster.local"' | sudo tee -a /etc/hosts')




kubectl apply --filename https://storage.googleapis.com/tekton-releases/pipeline/previous/v0.38.3/release.yaml
kubectl apply --filename https://github.com/shipwright-io/build/releases/download/v0.11.0/release.yaml
kubectl apply --filename https://github.com/shipwright-io/build/releases/download/v0.11.0/sample-strategies.yaml




kubectl apply -f helpers/argocd -n argocd




minikube tunnel



echo "$(kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d)"



