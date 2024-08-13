FROM nvidia/cuda:11.3.1-devel-ubuntu20.04

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && \
     apt-get install -y \
     wget \
     build-essential \
     g++ \
     gcc \
     libgl1-mesa-glx \
     libglib2.0-0 \
     openmpi-bin \
     openmpi-common \
     libopenmpi-dev \
     libgtk2.0-dev \
     git && \
     apt-get clean && \
     rm -rf /var/lib/apt/lists/*


# Install miniconda
ENV CONDA_DIR /opt/conda
RUN wget --quiet https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh && \
     /bin/bash ~/miniconda.sh -b -p /opt/conda
# Put conda in path so we can use conda activate
ENV PATH=$CONDA_DIR/bin:$PATH

# Copy the package
COPY . /root/bevfusion
# Navigate to the package
WORKDIR /root/bevfusion
# Create the Conda environment
RUN conda env create -f environment.yml && conda clean -ay

# Install the package
RUN . ~/.bashrc && \
     conda init && \
     . ~/.bashrc && \
     conda activate bevfusion && \
     echo "conda activate bevfusion" >> ~/.bashrc
#RUN python setup.py develop