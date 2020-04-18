```bash
export $OPERATOR_NAME=sample-operator
operator-sdk new $OPERATOR_NAME --api-version=sample.com/v1 --kind SampleApp --type helm
cd sample-operator
cp build/Dockerfile .
docker build -t pamir/sample-helm-operator:0.0.1 .
docker push pamir/nginx-helm-operator:0.0.1
kubectl apply -f -R deploy/
```

References:
- https://www.openshift.com/blog/make-a-kubernetes-operator-in-15-minutes-with-helm
- https://github.com/operator-framework/operator-sdk/blob/master/doc/helm/user-guide.md
- https://github.com/operator-framework/operator-sdk
- https://github.com/operator-framework/operator-sdk/tree/v0.8.1
- https://www.youtube.com/watch?v=1on_wRY2dzQ