# docker-swift

### An Ubuntu 16.04 Docker image for [Swift](https://swift.org).

#### You can find the Docker Hub repo here: [https://hub.docker.com/r/chasontang/swift/](https://hub.docker.com/r/chasontang/swift/)

### Docker Instructions

##### Pull the Docker Image From Docker Hub:

```bash
docker pull chasontang/swift
```

##### Create a Container from the Image and Attach It:

```bash
docker run --privileged -i -t --name swiftfun chasontang/swift:3.0.1 /bin/bash
```

##### To Start and Attach Your Image Later:

Start your image with name `swiftfun`

```bash
docker start swiftfun
```

and then attach it

```bash
docker attach swiftfun
```