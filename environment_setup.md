Environment Setup
===

## Basic idea requirements

- Reference slides (zy_handover/2_Meeting_slides/Tutorial/ciw_docker_environment.pptx)

- Flow of create container
1. Find proper image you want https://hub.docker.com/r/tensorflow/tensorflow/tags?page=2&name=2.0
2. Log in work station (host): 
```
(sudo) docker pull tensorflow/tensorflow:2.0.0-gpu-py3
```
3. Make sure docker is exist
```
docker image ls
```
4. Create container
```
docker run -it (--rm) --gpus "device=0,1" --name zy_PRNet_tensorboard --ipc=host -v /srv:/srv -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=$DISPLAY --env QT_X11_NO_MITSHM=1 -p 8080:8080 tensorflow/tensorflow:2.0.0-gpu-py3
```
- tensorflow/tensorflow:2.0.0-gpu-py3 can place to any image name => REPOSITORY:TAG
- --gpus all          : how many gpu you will use
- -it               
- --name XXXXXXX      : name container
- -v /srv..........   : mount host path into container
- -p XX:XX            : tensorboard port
- 最後記得改成自己的tensorflow,還可以額外再加上自己想要的指令

5. Other command
```
# Check all container
docker ps -a
# start container (every reboot)
docker start container_id
# stop docker
exit
# Into container
docker exec -it container_name bash
```
6. Tensorboard (local suggested)
```
tensorboard --logdir=D:\Mnist_tensorflow_practice/Tensorboard --port=8080
http://localhost:8080/
(6060會遇防火牆)
```

### Hardware

- Nvidia GPU available

```
nvidia-smi
```

## Create new enviroment

### PRNet enviroment
- Commit image from [vlsilab docker](https://www.docker.com/get-started)
	- Sign in: vlsilab / vlsi95514
	- Find image: vlsilab/zy_PRNet

### Img2posGAN enviroment
- Commit image from [vlsilab docker](https://www.docker.com/get-started)
	- Sign in: vlsilab / vlsi95514
	- Find image: vlsilab/zy_pix2pix


## Existing enviroment

### PRNet enviroment on work station 102 
- Start and execute docker:
```
docker start zy_prnet_tb_gpu2
docker exec -it zy_prnet_tb_gpu2 bash
# for training
cd /srv/big_data/zy/PRNet_tensorflow
# for testing
cd /srv/big_data/zy/PRNet-master
```

### Img2posGAN enviroment on work station 111
- Start and execute docker:
```
docker start zy_ pix2pix 
docker exec -it zy_pix2pix bash
# for both training and testing
cd /srv/ssd1/zy/pix2pix-tensorflow-master
```


