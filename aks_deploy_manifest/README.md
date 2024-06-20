### Backstage deployment on AKS

[Backstage on AKS](https://backstage.io/docs/deployment/k8s)

### Build and push the image to ACR

```
# Build the container image from the Dockerfile

DOCKER_BUILDKIT=1 docker image build -t centralusacr.azurecr.io/backstage/backstage:1.21.1-13 .

# Login to Azure and ACR

az login
az acr login --n centralusacr

# Push the dockr image to ACR

docker push centralusacr.azurecr.io/backstage/backstage:1.21.1
```
### Login to the AKS cluster

```
# get aks credentials

$ az aks get-credentials --resource-group  centralus-rg --name aks-sbx 

# apply all the manifest file

$ kubectl apply -f backstage-secrets.yaml
$ kubectl apply -f postgres-secrets.yaml
$ kubectl apply -f backstage.yaml
$ kubectl apply -f backstage-service.yaml

```
