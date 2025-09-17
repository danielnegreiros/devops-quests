- Build dependencies

```bash
helm dependency build
```

- Install
```bash
n=networking
helm upgrade --install ingress-nginx ./ -f ./values.yaml -n=$n --create-namespace
```

