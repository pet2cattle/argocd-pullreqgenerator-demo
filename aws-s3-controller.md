

```
k create ns aws-controllers

cd tmp
git clone https://github.com/aws-controllers-k8s/s3-controller
cd ..

helm install s3controller tmp/s3-controller/helm/ -n aws-controllers
```

```
export DEMO_AWS_DEFAULT_REGION=us-west-2
```

(secrets/aws.sh)



## IRSA workaround

```
kubectl set env deployment/s3controller-s3-chart AWS_ACCESS_KEY_ID="$DEMO_AWS_ACCESS_KEY_ID" -n aws-controllers
kubectl set env deployment/s3controller-s3-chart AWS_SECRET_ACCESS_KEY="$DEMO_AWS_SECRET_ACCESS_KEY" -n aws-controllers
kubectl set env deployment/s3controller-s3-chart AWS_REGION="$DEMO_AWS_DEFAULT_REGION" -n aws-controllers
```



```
k get pods -n aws-controllers
```


```
k apply -f helpers/s3controller
```


```
awstools s3 list
```

```
k delete -f helpers/s3controller
```



```
awstools s3 list
```





## uninstall


helm uninstall s3controller -n aws-controllers


