# Run Nexus Repository OSS to your server

## 1. Run Nexus Repository OSS using container

```bash
podman run -d \
  --name nexus-service \
  -p 8081:8081 \
  -v nexus-volume:/nexus-data \
  sonatype/nexus3
```

To monitor setup proses run log command `podman logs -f nexus`

## 2. Nexus Repository OSS setup
