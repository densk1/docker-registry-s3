# Docker Registry with DO spaces S3 bucket



Taking the config file built into dockers registry image from `/etc/docker/registry/config.yml`, and adding the s3 related config into the file

>> NOTE: This has **NO** configured security!

## Useful Links
- https://docs.docker.com/registry/configuration/
- https://mfojtik.io/posts/digitalocean-spaces-registry/

### Start registry
```bash
docker run -d -p 5000:5000 \
  --restart=always \
  --name registry \
  -v `pwd`/config.yml:/etc/docker/registry/config.yml \
  registry:2
```

### Stop and Remove Registry
```bash
docker container stop registry && docker container rm -v registry
```

## Image Management

### Tag Image for local registry
`docker image tag ubuntu localhost:5000/ubuntu`

### Push image to local registry
`docker push localhost:5000/ubuntu`

### Pull image from local registry
`docker pull localhost:5000/ubuntu`

### List images in registry
`curl -X GET http://localhost:5000/v2/_catalog`