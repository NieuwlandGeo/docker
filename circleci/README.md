# Build and publish

```
docker build -t nieuwlandgeo/circleci:0.0.7 .
docker login
docker push nieuwlandgeo/circleci:0.0.7
```

To look inside:

```
docker run -it nieuwlandgeo/circleci:0.0.7 bash
```
