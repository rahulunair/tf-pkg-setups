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

FROM clearlinux:latest

LABEL maintainer="rahul.unnikrishnan.nair@intel.com"

ENV http_proxy http://proxy-us.intel.com:911
ENV https_proxy http://proxy-us.intel.com:912

RUN swupd update
RUN swupd bundle-add --skip-diskspace-check git vim \
    python-extras \
    performance-tools \
    c-basic \
    os-core-dev \
    java-basic \
    cloud-native-basic \
    os-clr-on-clr



RUN ln -s -f /usr/bin/python3 /usr/bin/python
RUN ln -s -f /usr/bin/pip3 /usr/bin/pip


RUN pip install \
          ipython \
          six numpy wheel mock \
          keras_applications \
          keras_preprocessing


RUN git clone https://github.com/rahulunair/benchmarks
RUN wget https://github.com/tensorflow/tensorflow/archive/v1.11.0.tar.gz && \
         tar zxvpf v1.11.0.tar.gz && \
         rm v1.11.0.tar.gz


CMD [ "/bin/bash" ]
