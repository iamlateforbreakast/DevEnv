# Create containers for development

Create a Dockerfile

```
FROM docker.io/library/debian:testing

LABEL com.github.containers.toolbox="true" \
      com.github.debarshiray.toolbox="true"

RUN apt-get update && \
    apt-get -y install sudo libcap2-bin && \
    apt-get clean

RUN sed -i -e 's/ ALL$/ NOPASSWD:ALL/' /etc/sudoers

RUN touch /etc/localtime
RUN echo VARIANT_ID=container >> /etc/os-release

CMD /bin/bash
```

Build the image

```
podman build -t debian-toolbox -f Dockerfile.debian
```

Create the toolbox container.

```
toolbox create -i localhost/debian-toolbox:latest
```
