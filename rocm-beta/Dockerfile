FROM rocm/dev-ubuntu-20.04:5.2.3

# Avoid annoying cmake -> tzdata install prompt
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get -y update && apt-get -y install \
    hipfft rocfft \
    git \
    cmake \
    libgtest-dev \
    openmpi-bin libopenmpi-dev \
    libhdf5-serial-dev

# Needed to trick ROCm into thinking there's a GPU
RUN echo "gfx90a" | sudo tee --append $(hipconfig -R)/bin/target.lst

# Needed by Cholla Makefile
ENV CHOLLA_MACHINE=github
ENV HDF5_ROOT=/usr/lib/x86_64-linux-gnu/hdf5/serial/
ENV MPI_ROOT=/usr/lib/x86_64-linux-gnu/openmpi/

ENV HIPCONFIG=/opt/rocm-5.2.3
ENV ROCM_PATH=/opt/rocm-5.2.3

#HIPFFT_PATH is not used anywhere
# These attempts do not work:
#ENV HIPCONFIG=$(hipconfig -C)
#ENV ROCM_PATH=$(hipconfig -R)
#RUN export HIPCONFIG='$(hipconfig -C)'
#RUN export ROCM_PATH='$(hipconfig -R)'

# Install hipRand
RUN git clone https://github.com/ROCmSoftwarePlatform/rocRAND.git && \
    cd rocRAND; mkdir build; cd build && \
    git submodule update --init && \
    cmake -DCMAKE_CXX_COMPILER=hipcc ../. && \
    make -j2 && \
    make install

	