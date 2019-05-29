#-------------------------------------------------------------------------------------------------------------
# Copyright (c) Microsoft Corporation. All rights reserved.
# Licensed under the MIT License. See https://go.microsoft.com/fwlink/?linkid=2090316 for license information.
#-------------------------------------------------------------------------------------------------------------

FROM continuumio/miniconda3

# Install git, process tools
RUN apt-get update && apt-get -y install git procps

RUN mkdir /workspace
WORKDIR /workspace

# Install pylint
RUN pip install pylint

# Install Python dependencies from requirements.txt if it exists
COPY .devcontainer/environment.yml.temp environment.yml* /workspace/
RUN if [ -f "environment.yml" ]; then conda env update base -f environment.yml && rm environment.yml*; fi

# Clean up
RUN apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*

# Install prodigy
RUN mkdir /prodigy
WORKDIR /prodigy
COPY .devcontainer/prodigy-1.8.2-cp35.cp36.cp37-cp35m.cp36m.cp37m-linux_x86_64.whl /prodigy/prodigy-1.8.2-cp35.cp36.cp37-cp35m.cp36m.cp37m-linux_x86_64.whl
RUN pip install prodigy-1.8.2-cp35.cp36.cp37-cp35m.cp36m.cp37m-linux_x86_64.whl

ENV PRODIGY_HOME /workspace
EXPOSE 8080

# Set the default shell to bash instead of sh
ENV SHELL /bin/bash

