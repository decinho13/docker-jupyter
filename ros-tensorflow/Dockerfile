# Copyright (c) Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.
ARG BASE_CONTAINER=decinho13/base-notebook:scipy
FROM $BASE_CONTAINER

USER root

LABEL maintainer="Dennis Lubczyk"
RUN apt-get update && apt-get install -y \
python-rosdep python-rosinstall gnupg2 curl ca-certificates\
&& apt-get clean

# Install ROS
RUN sh -c 'echo "deb http://packages.ros.org/ros/ubuntu xenial main" > /etc/apt/sources.list.d/ros-latest.list'
RUN apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 421C365BD9FF1F717815A3895523BAEEB01FA116
RUN apt-get update && apt-get install -y ros-kinetic-desktop-full \
 	&& rm -rf /var/lib/apt/lists/*

RUN pip install catkin_tools

# Configure ROS
RUN sudo rosdep init && sudo rosdep fix-permissions && rosdep update
RUN echo "source /opt/ros/kinetic/setup.bash" >> /root/.bashrc

# nvidia-container-runtime
ENV NVIDIA_VISIBLE_DEVICES all
ENV NVIDIA_DRIVER_CAPABILITIES compute,utility
ENV NVIDIA_REQUIRE_CUDA "cuda>=10.0 brand=tesla,driver>=384,driver<385"

ENV NCCL_VERSION 2.4.2

RUN wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/cuda-repo-ubuntu1604_10.0.130-1_amd64.deb
RUN sudo apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/7fa2af80.pub
RUN sudo apt-get update
RUN wget http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1604/x86_64/nvidia-machine-learning-repo-ubuntu1604_1.0.0-1_amd64.deb
RUN sudo apt install -y ./nvidia-machine-learning-repo-ubuntu1604_1.0.0-1_amd64.deb
RUN sudo apt-get update

    
RUN sudo apt-get update && \
        sudo apt-get install -y nvinfer-runtime-trt-repo-ubuntu1604-5.0.2-ga-cuda10.0 \
        && sudo apt-get update \
        && sudo apt-get install -y --no-install-recommends libnvinfer-dev=5.0.2-1+cuda10.0


# Install Tensorflow
RUN conda install --quiet --yes \
    'tensorflow=1.12*' \
    'keras=2.2*' \
    'tensorflow-gpu' \
    'theano' \
    'pytorch' \
    'pyspark' \
    'nltk' && \
    conda clean -tipsy 
RUN pip install elephas gym keras-rl
