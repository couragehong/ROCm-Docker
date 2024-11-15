# ROCm Docker Environment

This Docker environment is custom(?) setting dockerfile based on official [AMD ROCm Docker repository](https://github.com/ROCm/ROCm-docker) to test and develop HIP kernels in various AMD GPU environment.

## Prerequisites

- Docker installed on your system
- AMD GPU with ROCm support
- Docker with AMD GPU support configured

## Quick Start

### Building the Image
```bash
# Build the Docker image
docker build -f Dockerfile.rocm-6.2.0-ubuntu-22.04 -t rocm-6.2.0 .
```

If you encounter a Hash Sum mismatch error like this:  
```
=> ERROR [2/7] RUN export DEBIAN_FRONTEND=noninteractive && apt-get update -qq && apt-get install --no-install-recommends -y ca-certificates git locales-all make p 

=> ERROR [3/7] RUN mkdir -p /etc/apt/keyrings     && wget -q -O - https://repo.radeon.com/rocm/rocm.gpg.key | gpg --dearmor > /etc/apt/keyrings/rocm.gpg     && echo "deb [arch=amd64, signed-by=/etc/apt/keyrings/rocm.gpg  ...
```
Simply try building the image again. This error is usually temporary and occurs due to package repository synchronization issues.


## Running the Container
```
# Run the container with GPU support
sudo docker run -it \
    --device=/dev/kfd \
    --device=/dev/dri \
    --group-add video \
    <image-name>
```


### AMD ROCm official document
- ROCm-docker (https://github.com/ROCm/ROCm-docker)
- Running ROCm Docker containers (https://rocm.docs.amd.com/projects/install-on-linux/en/latest/how-to/docker.html)



