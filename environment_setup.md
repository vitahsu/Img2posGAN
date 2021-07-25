Environment Setup
===

## Basic idea requirements
- Reference slides (zy_handover/2_Meeting_slides/Tutorial/ciw_docker_environment.pptx)

#### Hardware

- Nvidia GPU available

```
nvidia-smi
```

#### Host OS: Linux
- Recommended: Ubuntu 18.04 LTS

#### Docker with nvidia-container-toolkit

- Docker installation on ubuntu
    - https://docs.docker.com/engine/install/ubuntu/
- nvidia-container-toolkit installation on ubuntu
    - https://github.com/NVIDIA/nvidia-docker

- Check docker installation

```
docker version
```

## PyTorch environment

- Check nvidia-container-toolkit installation with pytorch image

```
# pull image
docker pull pytorch/pytorch:1.2-cuda10.0-cudnn7-devel

# (option 1) run container (basic)
docker run -it --rm --name my-pt-1.2 --gpus '"device=0"' --ipc=host pytorch/pytorch:1.2-cuda10.0-cudnn7-devel

# (option 2) run container (mount /srv (host) to /srv (container))
docker run -it --rm --gpus '"device=0"' --name my-pt-1.2 --ipc=host -v /srv:/srv pytorch/pytorch:1.2-cuda10.0-cudnn7-devel

# (option 3) run container (mount /srv (host) to /srv (container), GUI related arguments)
docker run -it --rm --gpus '"device=0"' --name my-pt-1.2 --ipc=host -v /srv:/srv -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=$DISPLAY --env QT_X11_NO_MITSHM=1 pytorch/pytorch:1.2-cuda10.0-cudnn7-devel

# check requirements inside the container
# check available GPUs
nvidia-smi

# check pytorch version
python -c 'import torch; print(torch.__version__)'
```

- Manage conda in official pytorch image (optional)

```
conda init
source ~/.bashrc
# now you should see (base) in terminal
```

## Other packages (in pytorch container)

- OpenCV

```
# choose the following one only

# pip
pip install opencv-python

# conda
conda install -c conda-forge opencv
```

- OpenCV common issues

```
# libSM.so.6
apt update
apt install -y libsm6 libxext6 libxrender-dev

# libSM.so.6, libgtk-x11-2.0.so.0, libgthread-2.0.so.0
apt update
apt install libgtk2.0-dev

# libGL.so.1
apt update
apt install libgl1-mesa-glx
```

- easydict

```
pip install easydict
```

- ptflops

```
pip install ptflops
```

- graphviz

```
apt install graphviz
```

- Test GUI in docker environment using OpenCV (optional)

```
# first, use the following command outside the container
xhost local:root
```

```
# create and run the following example
import cv2

img = cv2.imread('test.jpg')
cv2.imshow('img', img)
cv2.waitKey()
cv2.destroyAllWindows()
```
