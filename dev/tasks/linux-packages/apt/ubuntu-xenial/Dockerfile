# Licensed to the Apache Software Foundation (ASF) under one
# or more contributor license agreements.  See the NOTICE file
# distributed with this work for additional information
# regarding copyright ownership.  The ASF licenses this file
# to you under the Apache License, Version 2.0 (the
# "License"); you may not use this file except in compliance
# with the License.  You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing,
# software distributed under the License is distributed on an
# "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
# KIND, either express or implied.  See the License for the
# specific language governing permissions and limitations
# under the License.

ARG FROM=ubuntu:xenial
FROM ${FROM}

COPY qemu-* /usr/bin/

RUN \
  echo "debconf debconf/frontend select Noninteractive" | \
    debconf-set-selections

ARG DEBUG

RUN \
  quiet=$([ "${DEBUG}" = "yes" ] || echo "-qq") && \
  apt update ${quiet} && \
  apt install -y -V ${quiet} \
    gnupg \
    wget && \
  wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key | apt-key add - && \
  echo "deb http://apt.llvm.org/xenial/ llvm-toolchain-xenial-7 main" > \
    /etc/apt/sources.list.d/llvm.list && \
  apt update ${quiet} && \
  apt install -y -V ${quiet} \
    autoconf-archive \
    bison \
    build-essential \
    cmake \
    debhelper\
    devscripts \
    dh-autoreconf \
    flex \
    git \
    gtk-doc-tools \
    libboost-filesystem-dev \
    libboost-regex-dev \
    libboost-system-dev \
    libbrotli-dev \
    libdouble-conversion-dev \
    libgirepository1.0-dev \
    libglib2.0-doc \
    libgoogle-glog-dev \
    liblz4-dev \
    libprotobuf-dev \
    libprotoc-dev \
    libre2-dev \
    libsnappy-dev \
    libssl-dev \
    lsb-release \
    pkg-config \
    protobuf-compiler \
    python3-dev \
    python3-numpy && \
  if apt list | grep '^clang-7/'; then \
    apt install -y -V ${quiet} clang-7; \
  fi && \
  if apt list | grep '^nvidia-cuda-toolkit/'; then \
    apt install -y -V ${quiet} nvidia-cuda-toolkit; \
  fi && \
  apt clean && \
  rm -rf /var/lib/apt/lists/*
