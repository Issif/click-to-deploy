falco-docker
============

Dockerfile source for Falco [docker](https://docker.io) image.

# Upstream

This source repo was originally copied from:
https://github.com/falcosecurity/falco/tree/master/docker/falco


# Disclaimer

This is not an official Google product.

# <a name="about"></a>About

This image contains an installation of Falco

For more information, see the
[Official Image Marketplace Page](https://console.cloud.google.com/marketplace/product/google/falco).

### Prerequisites

Configure [gcloud](https://cloud.google.com/sdk/gcloud/) as a Docker credential helper:

```shell
gcloud auth configure-docker
```
### Pull command

```shell
docker -- pull marketplace.gcr.io/google/falco
```
Dockerfile for this image can be found [here](https://github.com/GoogleCloudPlatform/click-to-deploy/tree/master/docker/falco/0/debian12/0.40/).

### Running Falco

To run Falco in a container using Docker use the following commands:

- The preferred way is to use the modern eBPF probe driver:
  ```shell
  docker run --rm -i -t \
    --privileged \
    -v /var/run/docker.sock:/host/var/run/docker.sock \
    -v /proc:/host/proc:ro \
    -v /boot:/host/boot:ro \
    -v /lib/modules:/host/lib/modules:ro \
    -v /usr:/host/usr:ro \
    -v /etc:/host/etc:ro \
    marketplace.gcr.io/google/falco -o engine.kind=modern_ebpf
  ```

- Alternatively, you can use the legacy eBPF probe driver:
  ```shell
  docker run --rm -i -t \
    --privileged \
    -v /var/run/docker.sock:/host/var/run/docker.sock \
    -v /proc:/host/proc:ro \
    -v /boot:/host/boot:ro \
    -v /lib/modules:/host/lib/modules:ro \
    -v /usr:/host/usr:ro \
    -v /etc:/host/etc:ro \
    marketplace.gcr.io/google/falco -o engine.kind=ebpf
  ```

- Or the the Kernel module driver:
  ```shell
  docker run --rm -i -t \
    --privileged \
    -v /var/run/docker.sock:/host/var/run/docker.sock \
    -v /dev:/host/dev \
    -v /proc:/host/proc:ro \
    -v /boot:/host/boot:ro \
    -v /lib/modules:/host/lib/modules:ro \
    -v /usr:/host/usr:ro \
    -v /etc:/host/etc:ro \
    marketplace.gcr.io/google/falco 
  ```

**NOTE:** Depending on your Linux distribution, you may need to install the Linux Kernel headers package for your kernel version.

Debian GNU/Linux 12 (bookworm):

```shell
sudo apt install linux-headers-$(uname -r)
```

For more information on running Falco within Docker, see the official [Falco documentation - Run within Docker](https://falco.org/docs/setup/container/).
