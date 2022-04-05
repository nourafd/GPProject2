ARG PYTORCH="1.5"
ARG CUDA="10.1"
ARG CUDNN="7"

FROM ubuntu:18.04
RUN apt update
RUN apt install software-properties-common -y
RUN add-apt-repository ppa:graphics-drivers 
RUN apt install nvidia-driver-440 -y


FROM pytorch/pytorch:${PYTORCH}-cuda${CUDA}-cudnn${CUDNN}-devel

ENV TORCH_CUDA_ARCH_LIST="6.0 6.1 7.0+PTX"
ENV TORCH_NVCC_FLAGS="-Xfatbin -compress-all"
ENV CMAKE_PREFIX_PATH="$(dirname $(which conda))/../"


RUN apt-get update && apt-get install -y git libglib2.0-0 libsm6 libxrender-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN apt-get update
RUN apt-get install ffmpeg libsm6 libxext6  -y




# Install mmfashion
RUN conda clean --all
RUN git clone --recursive https://github.com/nourafd/GPProject2.git /gp1997
WORKDIR /gp1997
ENV FORCE_CUDA="1"
ENV CUDA_HOME="/usr/lib/nvidia-cuda-toolkit"
RUN pip install -r requirements.txt
RUN pip install --no-cache-dir -e .
