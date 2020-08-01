FROM fedora:29

RUN dnf -y update
RUN dnf -y install gcc make automake gcc-c++
RUN dnf -y install pciutils which kmod
RUN dnf -y install wget
RUN wget https://kojipkgs.fedoraproject.org/repos-dist/coreos-pool/latest/x86_64/Packages/k/kernel-devel-5.7.8-200.fc32.x86_64.rpm
RUN yum -y localinstall kernel-devel-5.7.8-200.fc32.x86_64.rpm
RUN wget http://developer.download.nvidia.com/compute/cuda/11.0.2/local_installers/cuda_11.0.2_450.51.05_linux.run

# Unload kernel modules if previously loaded. Ignore errors if modules aren't loaded yet.
RUN rmmod nvidia_drm || true
RUN rmmod nvidia_modeset || true
RUN rmmod nvidia || true

# Install NVIDIA drivers.
# - ignore compiler check
# - silent installation without user interaction
RUN sh cuda_11.0.2_450.51.05_linux.run --override --kernel-source-path=/usr/src/kernels/5.7.8-200.fc32.x86_64/ --silent --driver --samples --toolkit

# Test logfile for errors.
RUN cat /var/log/nvidia-installer.log

# https://docs.nvidia.com/cuda/cuda-quick-start-guide/index.html
ENV PATH=/usr/local/cuda-11.0/bin${PATH:+:${PATH}}
ENV LD_LIBRARY_PATH=/usr/local/cuda-11.0/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}

# Build and run example.
RUN cuda-install-samples-11.0.sh ~
WORKDIR ~/NVIDIA_CUDA-11.0_Samples/0_Simple/vectorAdd
RUN make
RUN ./vectorAdd
