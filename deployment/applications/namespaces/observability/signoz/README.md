```bash
telemetrygen traces \
  --otlp-endpoint 10.10.100.191:30439 \
  --otlp-insecure \
  --traces 1 \
  --workers 1 \
  --interval 1s \
  --child-spans 5 \
  --marshal \
  --status-code 2 \
  --telemetry-attributes http.status_code=202 \
  --telemetry-attributes http.method=\"GET\"


telemetrygen logs \
  --otlp-endpoint 10.10.100.191:30439 \
  --otlp-insecure \
  --duration 5s \
  --body "correlated log example" \
  --trace-id 38a91b1f68c3a79941bf9d2ecc3da026 \
  --span-id 032f2ac14d9334f4 \
  --rate 1 \
  --workers 1
```