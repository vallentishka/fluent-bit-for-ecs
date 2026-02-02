# Build Cheatsheet

## Build and Push to GHCR (amd64)

```bash
# Build and push
docker buildx build \
  --platform linux/amd64 \
  --build-arg flb_upstream_version=4.0.3 \
  -t ghcr.io/vallentishka/fluent-bit-for-ecs:0.1.0-flb-4.0.3 \
  --push \
  .
```

## Get Digest

```bash
docker manifest inspect ghcr.io/vallentishka/fluent-bit-for-ecs:0.1.0-flb-4.0.3 | grep -A2 '"digest"' | head -3
```

Or full reference:
```bash
docker inspect --format='{{index .RepoDigests 0}}' ghcr.io/vallentishka/fluent-bit-for-ecs:0.1.0-flb-4.0.3
```

## Update oasis-ecs Dockerfile

Edit `projects/oasis-ecs/containers/firelens/Dockerfile`:
```dockerfile
FROM ghcr.io/vallentishka/fluent-bit-for-ecs:0.1.0-flb-4.0.3@sha256:<digest>
```

## Build New Fluent Bit Version

Change `flb_upstream_version` and tag:
```bash
docker buildx build \
  --platform linux/amd64 \
  --build-arg flb_upstream_version=4.0.3 \
  -t ghcr.io/vallentishka/fluent-bit-for-ecs:0.1.0-flb-4.0.3 \
  --push \
  .
```
