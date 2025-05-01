# A RAG File Normalization service on Kubernetes ( GKE )

This project deploys `docling-serve` on a private GKE cluster namespace (`docling`) without exposing it to the internet. You can test it by accessing a pod in the same subnet via `kubectl exec` or using a bastion.

## Deploy Steps

```bash
make deploy
```

## Create GPU Node Pool

To create a GPU node pool in your GKE cluster, use the following command:

```bash
gcloud container node-pools create gpu-pool \
  --accelerator type=nvidia-tesla-t4,count=1 \
  --zone <your-cluster-zone> \
  --cluster <your-cluster-name> \
  --num-nodes=1 \
  --min-nodes=1 \
  --max-nodes=3 \
  --enable-autoscaling
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
