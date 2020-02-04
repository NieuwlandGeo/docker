# Usage

Our image for testing wgp5

# Build and publish

## Manual

```
docker build -t nieuwlandgeo/docker:7.3-cli-node-browsers .
docker login
docker push nieuwlandgeo/docker:7.3-cli-node-browsers
```

Run container:

```
docker run -it nieuwlandgeo/docker:7.3-cli-node-browsers bash
```

## Automated

https://docs.docker.com/docker-hub/github/
