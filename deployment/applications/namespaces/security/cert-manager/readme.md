```bash
helm template \
  cert-manager oci://quay.io/jetstack/charts/cert-manager:v1.18.2 \
  --set crds.enabled=true \
  > tempaltes/cert-manager.yaml
  ``` 