##########################################################################
# Build env for Tensorflow using MKL and Anaconda Python 3.7 on Clear linux
# How to run this?
# Download this file and rename to `Dockerfile`
# docker build -t tf-mkl-cpu .
# docker run -it tf-mkl-cpu
# conda activate tf-env
# python benchmarks/scripts/tf_cnn_benchmarks/tf_cnn_benchmarks.py  \
# --device=cpu --batch_size=32 --model=alexnet --data_format=NHWC
############################################################################

FROM ubuntu:bionic

LABEL maintainer="rahul.unnikrishnan.nair@intel.com"
ARG TF_BRANCH="v1.12.0-rc0"

ENV PATH /opt/conda/bin:$PATH
ENV http_proxy http://proxy-us.intel.com:911
ENV https_proxy http://proxy-us.intel.com:912

RUN \
  apt-get  update -y && \
  apt-get install -y git wget gzip \
    curl python3-dev \
    python3-pip build-essential \
    vim openjdk-8-jdk \
    gcc-multilib libomp-dev \
    linux-tools-common gawk \
    && rm -rf /var/lib/lists/*

RUN ln -s /usr/bin/python3 /usr/bin/python
RUN ln -s /usr/bin/pip3 /usr/bin/pip

# configure bazel repo and install bazel
RUN touch /etc/apt/sources.list.d/bazel.list && \
echo "deb [arch=amd64] http://storage.googleapis.com/bazel-apt stable jdk1.8" \
  > /etc/apt/sources.list.d/bazel.list
RUN curl https://bazel.build/bazel-release.pub.gpg | apt-key add - && \
    apt-get update &&  \
    apt-get install -y bazel

RUN pip install \
          ipython \
          six numpy wheel mock \
          keras_applications \
          keras_preprocessing 


RUN wget https://github.com/tensorflow/tensorflow/archive/v1.11.0.tar.gz \
      && tar zxvpf v1.11.0.tar.gz && rm v1.11.0.tar.gz
CMD [ "/bin/bash" ]
