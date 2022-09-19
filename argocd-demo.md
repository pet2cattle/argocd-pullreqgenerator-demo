
```
k create ns argocd
helm repo add argo https://argoproj.github.io/argo-helm
helm install argocd argo/argo-cd -n argocd -f helpers/argocd_values.yaml
```



```
kubectl apply --filename https://storage.googleapis.com/tekton-releases/pipeline/previous/v0.38.3/release.yaml
kubectl apply --filename https://github.com/shipwright-io/build/releases/download/v0.11.0/release.yaml
kubectl apply --filename https://github.com/shipwright-io/build/releases/download/v0.11.0/sample-strategies.yaml
```

```
k create ns demoapp
```

```
kubectl apply -f helpers/argocd -n argocd
```


```
echo "$(kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d)"
```


