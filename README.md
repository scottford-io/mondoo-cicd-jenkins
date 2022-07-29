# Mondoo CI/CD - Jenkins

This repository is used to provide an example of integrating [Mondoo]() security scanning into a Jenkins CI pipeline. This example builds a [Python Flask App]() as a Docker container and publishes it to Docker Hub.

## Build the app

To build the app, simply run

```bash
docker build . -t <your tag>
```

**Example**

```bash
docker build . -t thesecureautomator/python-flask-app-demo
[+] Building 12.7s (17/17) FINISHED                                                                                                                              
 => [internal] load build definition from Dockerfile                                                                                                        0.1s
 => => transferring dockerfile: 325B                                                                                                                        0.0s
 => [internal] load .dockerignore                                                                                                                           0.0s
 => => transferring context: 2B                                                                                                                             0.0s
 => resolve image config for docker.io/docker/dockerfile:1                                                                                                  2.5s
 => [auth] docker/dockerfile:pull token for registry-1.docker.io                                                                                            0.0s
 => CACHED docker-image://docker.io/docker/dockerfile:1@sha256:443aab4ca21183e069e7d8b2dc68006594f40bddf1b15bbd83f5137bd93e80e2                             0.0s
 => [internal] load build definition from Dockerfile                                                                                                        0.0s
 => [internal] load .dockerignore                                                                                                                           0.0s
 => [internal] load metadata for docker.io/library/python:3.7-alpine                                                                                        0.7s
 => [auth] library/python:pull token for registry-1.docker.io                                                                                               0.0s
 => [1/6] FROM docker.io/library/python:3.7-alpine@sha256:a035147200d19b31a12dff0cf2b9690e17775f2bc7365296a28e07341e1a048d                                  0.0s
 => [internal] load build context                                                                                                                           0.1s
 => => transferring context: 28.60kB                                                                                                                        0.1s
 => CACHED [2/6] WORKDIR /code                                                                                                                              0.0s
 => CACHED [3/6] RUN apk add --no-cache gcc musl-dev linux-headers                                                                                          0.0s
 => [4/6] COPY requirements.txt requirements.txt                                                                                                            0.0s
 => [5/6] RUN pip install -r requirements.txt                                                                                                               7.8s
 => [6/6] COPY . .                                                                                                                                          0.0s
 => exporting to image                                                                                                                                      0.1s
 => => exporting layers                                                                                                                                     0.1s
 => => writing image sha256:b18f69952e8e0ab878cf0de58910e0b8d2052be14cca4c52b168e53fa9b5b7a8                                                                0.0s
 => => naming to docker.io/thesecureautomator/python-flask-app-demo
 ```

