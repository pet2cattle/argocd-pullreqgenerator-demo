


## Install in-cluster test vault

```
k create ns testvault
helm repo add testvault https://pet2cattle.github.io/helm-testvault/
helm install testvault testvault/testvault -n testvault
```

# store secret

```
k exec -it testvault-vaultcli -- sh -c "echo test | vault login -; vault kv put -mount=secret demo hello=world; vault kv get -mount=secret demo"
```





k apply -f helpers/eso/vault/cluster-store.yaml






