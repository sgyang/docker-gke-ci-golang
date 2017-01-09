# gke-ci-golang

Useful Docker image with golang, docker, gcloud, and kubectl for CI on GKE.

## Example

Run image with mounting docker socket file and service account key file:

```
docker run \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v /path/to/service-account/key.json:/etc/key.json \
    sgyang/gke-ci-golang:1.7
```

Test, build, push, and deploy a service:

```
# Test
go test -v .

# Build
go build -o main .
docker build -t gcr.io/$PROJECT_ID/$NAME:$GIT_COMMIT .

# Push
gcloud auth activate-service-account --key-file /etc/key.json
gcloud docker -- push gcr.io/$PROJECT_ID/$NAME:$GIT_COMMIT

# Deploy
gcloud container clusters get-credentials $CLUSTER_NAME --project $PROJECT_ID --zone $ZONE
kubectl --namespace $NAMESPACE set image deployment/$NAME $NAME=gcr.io/$PROJECT_ID/$NAME:$GIT_COMMIT
```
