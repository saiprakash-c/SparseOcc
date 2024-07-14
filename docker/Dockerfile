ARG PYTORCH="1.11.0"
ARG CUDA="11.3"
ARG CUDNN="8"

FROM pytorch/pytorch:${PYTORCH}-cuda${CUDA}-cudnn${CUDNN}-devel

ENV TORCH_CUDA_ARCH_LIST="6.0 6.1 7.0 7.5 8.0 8.6+PTX" \
    TORCH_NVCC_FLAGS="-Xfatbin -compress-all" \
    CMAKE_PREFIX_PATH="$(dirname $(which conda))/../" \
    FORCE_CUDA="1"

# # Update the package list and install dependencies
# RUN apt-get update && \
#     apt-get install -y software-properties-common && \
#     add-apt-repository ppa:deadsnakes/ppa && \
#     apt-get update && \
#     apt-get install -y python3.8 python3.8-venv python3.8-dev python3.8-distutils && \
#     apt-get install -y curl && \
#     curl -sS https://bootstrap.pypa.io/get-pip.py | python3.8

# # Set Python 3.8 as the default Python version
# RUN update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.8 1 && \
#     update-alternatives --set python3 /usr/bin/python3.8

RUN apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/3bf863cc.pub \
    && apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1804/x86_64/7fa2af80.pub

RUN apt-get update && apt-get install -y ffmpeg libsm6 libxext6 git ninja-build libglib2.0-0 libsm6 libxrender-dev libxext6\
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Install MMCV, MMDetection and MMSegmentation
RUN pip install wandb
RUN pip install mmcv-full==1.6.0
RUN pip install mmdet==2.28.2
RUN pip install mmsegmentation==0.30.0

RUN apt-get update && apt-get install -y libturbojpeg
RUN pip install pyturbojpeg
RUN pip install pillow-simd==9.0.0.post1

# WORKDIR ../models/csrc
# RUN python setup.py build_ext --inplace

# Install MMDetection3D
# RUN conda clean --all
# RUN git clone https://github.com/open-mmlab/mmdetection3d.git -b v1.0.0rc6 /mmdetection3d
# WORKDIR /mmdetection3d
# RUN sed -i 's/numba==0.53.0/numba==0.55.0/' requirements/runtime.txt
# RUN pip install -r requirements/build.txt
# RUN pip install --no-cache-dir -e .
RUN pip install DCNv4
RUN pip install timm==0.6.11
RUN pip install opencv-python termcolor yacs pyyaml scipy
