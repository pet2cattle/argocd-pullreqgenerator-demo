




kubectl create secret generic aws-secret --from-literal=access-key=$DEMO_AWS_ACCESS_KEY_ID --from-literal=secret=$DEMO_AWS_SECRET_ACCESS_KEY -n external-secrets



k apply -f helpers/eso/aws/ssm.yaml


k get secretstore


awstools ssm set demo value --description "test ESO"





k apply -f helpers/eso/aws/externalsecret.yaml




k get externalsecret




k get secret es-aws-demo