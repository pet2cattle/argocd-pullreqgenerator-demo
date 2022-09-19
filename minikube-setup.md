


minikube addons enable registry
minikube addons enable ingress




minikube ssh cat /etc/hosts | grep registry.kube-system.svc.cluster.local >/dev/null 2>&1|| (kubectl get svc registry -n kube-system >/dev/null 2>&1 && minikube ssh echo "$(kubectl get svc registry -n kube-system -o jsonpath='{ .spec.clusterIP }') registry.kube-system.svc.cluster.local"' | sudo tee -a /etc/hosts')










minikube tunnel

