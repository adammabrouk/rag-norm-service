# A RAG File Normalization service on Kubernetes ( GKE )

This project deploys `docling-serve` on a private GKE cluster namespace (`docling`) without exposing it to the internet. You can test it by accessing a pod in the same subnet via `kubectl exec` or using a bastion.

## Deploy Steps

```bash
make deploy
```

## Access Pod Terminal
```bash
kubectl exec -n docling -it $(kubectl get pod -n docling -l app=docling-serve -o jsonpath='{.items[0].metadata.name}') -- /bin/sh
```

## Test Service
Inside the pod:
```sh
wget -qO- http://docling-service
```
