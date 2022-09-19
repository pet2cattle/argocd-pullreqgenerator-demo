
k create ns external-secrets
helm repo add external-secrets https://charts.external-secrets.io
helm install external-secrets external-secrets/external-secrets -n external-secrets --set installCRDs=true


k ns external-secrets

