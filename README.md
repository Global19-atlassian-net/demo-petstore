# Build Petstore example

## Clean, build, and re-deploy

Note: if using minikube, make sure you setup to use minikube Docker env, e.g. `eval $(minikube docker-env)`

```bash
IMAGE_REPO=petstore2-example
IMAGE_VERSION=2

docker build -t ${IMAGE_REPO}:${IMAGE_VERSION} .
helm template ../../charts/petstore --namespace default --set image.repository=${IMAGE_REPO},image.tag=${IMAGE_VERSION} | kubectl apply -f -

```

Cleanup

```bash
kubectl delete deployments,services -l chart=petstore2-v2 -ndefault
```