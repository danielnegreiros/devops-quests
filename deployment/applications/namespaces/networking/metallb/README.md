- Build dependencies

```bash
helm dependency build
```

- Install
```bash
helm upgrade --install metallb ./ -f ./values.yaml --create-namespace
```

