


kubectl create namespace crossplane-system

helm repo add crossplane-stable https://charts.crossplane.io/stable
helm repo update

helm install crossplane -n crossplane-system crossplane-stable/crossplane



k ns crossplane-system



while true; do k get crd | grep -i ControllerConfig >/dev/null 2>&1; if [ "$?" -eq 0 ]; then break; fi; sleep 10; done




k apply -f helpers/xplane/aws-provider.yaml



while true; do k get deploy -n crossplane-system | grep provider-aws >/dev/null 2>&1; if [ "$?" -eq 0 ]; then break; fi; sleep 10; done



export BASE64ENCODED_AWS_ACCOUNT_CREDS=$(echo -e "[default]\naws_access_key_id = $DEMO_AWS_ACCESS_KEY_ID\naws_secret_access_key = $DEMO_AWS_SECRET_ACCESS_KEY" | base64  | tr -d "\n")



cat <<EOF | k apply -f -
---
apiVersion: v1
kind: Secret
metadata:
  name: aws-account-creds
  namespace: crossplane-system
type: Opaque
data:
  creds: ${BASE64ENCODED_AWS_ACCOUNT_CREDS}
---
apiVersion: aws.crossplane.io/v1beta1
kind: ProviderConfig
metadata:
  name: aws-provider
  namespace: crossplane-system
spec:
  credentials:
    source: Secret
    secretRef:
      namespace: crossplane-system
      name: aws-account-creds
      key: creds
EOF



## bucket



k apply -f helpers/xplane/bucket/bucket.yaml -n crossplane-system


## rds secret


k apply -f helpers/xplane/rds/instance.yaml -n crossplane-system



k describe rdsinstance.database.aws.crossplane.io/xplane-demo-rds


k get secret xplane-con-secret -n crossplane-system




## composition


k apply -f helpers/xplane/composition/definition.yaml



k apply -f helpers/xplane/composition/implementation.yaml


k apply -f helpers/xplane/composition/instance.yaml






k describe sgallowoutgoing.pet2cattle.com/sgone






awstools ec2 sg list sg













