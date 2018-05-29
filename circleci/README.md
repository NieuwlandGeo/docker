# Usage

Our image for testing wgp5

# Build and publish

## Manual

```
docker build -t nieuwlandgeo/circleci:0.0.7 .
docker login
docker push nieuwlandgeo/circleci:0.0.7
```

Run container:

```
docker run -it nieuwlandgeo/circleci:0.0.7 bash
```

## Automated

https://docs.docker.com/docker-hub/github/
