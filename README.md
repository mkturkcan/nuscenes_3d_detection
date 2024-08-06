# 3D Detection with NuScenes
Environment setup script for Radar+Lidar+Camera integration with mmdetection3d.

## Environment Setup

It is important that we are running everything as root, under the /root/ directory. A lot of the files we are using have hardcoded paths. Change accordingly for the whole codebase if needed. Start by uploading v1.0-mini.tgz under /root/ and executing:
```console
tar -xvzf v1.0-mini.tgz
```
Then, if we have a working conda installation, we run the following, one line at a time, saying yes when prompted.
```console
conda create -n pytorch python=3.9
conda activate pytorch
conda install pytorch==2.0.0 torchvision==0.15.0 torchaudio==2.0.0 pytorch-cuda=11.8 cudatoolkit=11.8 -c pytorch -c nvidia
export CUDA_HOME=$CONDA_PREFIX
conda install nvidia/label/cuda-11.8.0::cuda-nvcc
export LD_LIBRARY_PATH="$CONDA_PREFIX/lib"
conda install nvidia/label/cuda-11.8.0::cuda-cudart
conda install nvidia/label/cuda-11.8.0::cuda-cudart-dev
conda install nvidia/label/cuda-11.8.0::libcusparse
conda install nvidia/label/cuda-11.8.0::libcusparse-dev
conda install nvidia/label/cuda-11.8.0::libcublas-dev
conda install nvidia/label/cuda-11.8.0::libcusolver-dev
pip install -U openmim
mim install mmcv-full==1.6.0

pip install mmdet==2.28.2
pip install mmsegmentation==0.30.0

git clone https://github.com/fundamentalvision/Deformable-DETR.git
cd Deformable-DETR/models/ops
pip install .
cd /root/
pip install lyft-dataset-sdk
conda install jupyterlab
pip install nuscenes-devkit
pip install trimesh
pip install tensorboard
pip install timm
conda install conda-forge::einops
conda install scikit-image
cd rcbevdet-master
python tools/create_data.py --root-path=/root/ --version="v1.0-mini" --max-sweeps=10 --dataset nuscenes 
python tools/create_data_nuscenes_RC.py --root-path=/root/ --version="v1.0-mini"
python tools/test.py configs/rcbevdet/det-256x704-r50-BEV128-9kf-depth-withHoP-cbgs12e-circlelarger.py det-256x704-r50-BEV128-9kf-depth-hop.pth --eval bbox
```
