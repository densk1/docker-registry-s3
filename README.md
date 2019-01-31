# Docker Registry with DO spaces S3 bucket



Taking the config file built into dockers registry image from `/etc/docker/registry/config.yml`, and adding the s3 related config into the file

>> NOTE: This has **NO** configured security!

## Useful Links
- https://docs.docker.com/registry/configuration/
- https://mfojtik.io/posts/digitalocean-spaces-registry/
- https://www.alibabacloud.com/blog/how-to-setup-docker-private-registry-on-ubuntu-16-04_594085

### Start registry
```bash
docker run -d -p 5000:5000 \
  --restart=always \
  --name registry \
  -v `pwd`/.htpasswd:/etc/nginx/.htpasswd \
  -v `pwd`/config.yml:/etc/docker/registry/config.yml \
  registry:2
```

### Stop and Remove Registry
```bash
docker container stop registry && docker container rm -v registry
```

## Image Management

### Tag Image for local registry
`docker image tag ubuntu sub.example.com/ubuntu`

### Push image to local registry
`docker push sub.example.com/ubuntu`

### Pull image from local registry
`docker pull sub.example.com/ubuntu`

### List images in registry
`curl -X GET http://sub.example.com/v2/_catalog`

## Securing registry

### `// .htpasswd`
You will be prompted to create a password:
`htpasswd -B .htpasswd $USERNAME_FOR_REGISTRY`

### login
`docker login https://sub.example.com`
