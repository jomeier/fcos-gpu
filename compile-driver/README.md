# Compile NVIDIA driver

* git clone https://github.com/jomeier/fcos-gpu.git
* cd fcos-gpu/compile-driver

## Build image with drivers
* podman build -t gpu -f Dockerfile .

## Install drivers
* podman run -it --privileged gpu install-drivers.sh
