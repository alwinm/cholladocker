FROM nvidia/cuda:11.7.1-devel-ubuntu22.04
# Needs to be devel, not base or runtime, to have nvcc
# Ubuntu 22 is better than 18 because Ubuntu 22 default git is > 2.17
# Github actions requires git > 2.17 so that cholla is pulled into a git repo
# Which is required for the Makefile
RUN apt-get -y update
RUN apt-get -y install git
# With ubuntu 22.04 this grabs 2.34.1

RUN apt install -y -q openmpi-bin libopenmpi-dev
RUN apt-get -y install libhdf5-serial-dev
RUN apt-get -y install cmake
RUN apt-get -y install libgtest-dev

ENV CUDA_ROOT=/usr/local/cuda-11/
ENV HDF5_ROOT=/usr/lib/x86_64-linux-gnu/hdf5/serial/
ENV MPI_ROOT=/usr/lib/x86_64-linux-gnu/openmpi/