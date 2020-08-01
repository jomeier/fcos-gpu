# Compile NVIDIA driver

* git clone https://github.com/jomeier/fcos-gpu.git
* cd fcos-gpu/compile-driver
* podman build -t gpu -f Dockerfile .
* podman run -it --privileged gpu install-drivers.sh
