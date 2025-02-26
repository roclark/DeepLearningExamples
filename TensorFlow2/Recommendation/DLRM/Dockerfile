# Copyright (c) 2021, NVIDIA CORPORATION. All rights reserved.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
# author: Tomasz Grel (tgrel@nvidia.com)


ARG FROM_IMAGE_NAME=nvcr.io/nvidia/tensorflow:21.06-tf2-py3
FROM ${FROM_IMAGE_NAME}

RUN pip install -e git+https://github.com/NVIDIA/dllogger#egg=dllogger

ENV HOROVOD_CYCLE_TIME=0.1

WORKDIR /dlrm

ADD . .

RUN mkdir -p /usr/local/lib/python3.8/dist-packages/tensorflow/include/third_party/gpus/cuda/ \
    && ln -s /usr/local/cuda/include /usr/local/lib/python3.8/dist-packages/tensorflow/include/third_party/gpus/cuda/ \
    && cd tensorflow-dot-based-interact \
    && make \
    && make pkg \
    && pip install ./artifacts/tensorflow_dot_based_interact-*.whl
