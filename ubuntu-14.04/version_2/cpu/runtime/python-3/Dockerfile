# Ubuntu 14.04
FROM ubuntu:14.04

LABEL maintainer "MICROSOFT CORPORATION" \
      com.microsoft.cntk.version="2.2"

ENV CNTK_VERSION="2.2"

RUN apt-get update && apt-get install -y --no-install-recommends \
    # General
        ca-certificates \
        wget \
        && \
    # Clean-up
    apt-get -y autoremove \
        && \
    rm -rf /var/lib/apt/lists/*

# Get CNTK Binary Distribution
RUN CNTK_VERSION_DASHED=$(echo $CNTK_VERSION | tr . -) && \
    CNTK_SHA256="98236d98259d881d489a13ecf2d6bc5d45df773feddc2db1f302614b6cb02d64" && \
    wget -q https://cntk.ai/BinaryDrop/CNTK-${CNTK_VERSION_DASHED}-Linux-64bit-CPU-Only.tar.gz && \
    echo "$CNTK_SHA256 CNTK-${CNTK_VERSION_DASHED}-Linux-64bit-CPU-Only.tar.gz" | sha256sum --check --strict - && \
    tar -xzf CNTK-${CNTK_VERSION_DASHED}-Linux-64bit-CPU-Only.tar.gz && \
    rm -f CNTK-${CNTK_VERSION_DASHED}-Linux-64bit-CPU-Only.tar.gz && \
    /bin/bash /cntk/Scripts/install/linux/install-cntk.sh --py-version 35 --docker

WORKDIR /root
