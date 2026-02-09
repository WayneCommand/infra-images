# infra-images
This is the list of mirrors used for infrastructure, providing the most versatile environment to standardize processes.

## Build

### ffmpeg
```shell
docker build -t infra-ffmpeg:latest ./ffmpeg
```

```shell
# push
docker tag infra-ffmpeg:latest ghcr.io/waynecommand/infra-images:ffmpeg-latest

echo '{token}' | docker login ghcr.io -u waynecommand --password-stdin

docker push ghcr.io/waynecommand/infra-images:ffmpeg-latest
```