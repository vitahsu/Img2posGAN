Environment Setup
===

## :large_orange_diamond: Basic idea requirements
### 
- Reference slides (zy_handover/2_Meeting_slides/Tutorial/ciw_docker_environment.pptx)

- Flow of create container
1. Find proper image you want https://hub.docker.com/r/tensorflow/tensorflow/tags?page=2&name=2.0
2. Log in work station (host): 
	```
	(sudo) docker pull tensorflow/tensorflow:2.0.0-gpu-py3
	```
3. Make sure docker is exist
	```
	docker images
	```
4. Create container
	```
	#  example on 102
	docker run -it --gpus "device=0,1" --name zy_PRNet_tensorboard --ipc=host -v /srv:/srv -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=$DISPLAY --env QT_X11_NO_MITSHM=1 -p 8080:8080 tensorflow/tensorflow:2.0.0-gpu-py3
	```
	> --gpus all          : how many gpu you will use<br>
	> -it               <br>
	> --name XXXXXXX      : name container<br>
	> -v /srv..........   : mount host path into container<br>
	> -p XX:XX            : tensorboard port<br>
	> tensorflow/tensorflow:2.0.0-gpu-py3 can place to any image name => REPOSITORY:TAG<br>

5. Other commands
	```
	# Check all containers
	docker ps -a
	# start container (every time reboot)
	docker start container_id
	# stop container
	docker stop container_id
	# exit container
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
	htop
	df -h
	```
<br>

## :large_orange_diamond: Create new enviroment

### PRNet enviroment
- Commit image from [vlsilab docker](https://www.docker.com/get-started)
	- Sign in: vlsilab / vlsi95514
	- Find image: vlsilab/zy_prnet:latest

### Img2posGAN enviroment
- Commit image from [vlsilab docker](https://www.docker.com/get-started)
	- Sign in: vlsilab / vlsi95514
	- Find image: vlsilab/zy_pix2pix:latest
- Example
	- test on 102
		```
		docker pull vlsilab/zy_pix2pix:latest
		# make sure pull image sucessfully
		docker images
		# create container
		docker run -it --gpus all --name zy_pix2pix_test --ipc=host -v /srv:/srv -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=$DISPLAY --env QT_X11_NO_MITSHM=1 vlsilab/zy_pix2pix:latest
		# make sure create container sucessfully
		docker ps -a 
		# try trainin code
		CUDA_VISIBLE_DEVICES=1 python img2pos_mask_with_export_v2_depress_DAE_EBGAN_lr_decay0.8_v2_lr5e5_0326_pretrainD_fix2_aug_cer10_45.py --mode train --checkpoint train_model_mask_DAE_0310_lr_decay0.8_v2_lr5e5_pretrain_b32 --output_dir 102_train_model_mask_DAE_EBGAN_0614_lr_decay0.8_v2_lr5e5_pretrainD_b32_fix2_aug_cer_cer10_45 --max_epochs 400 --input_dir /srv/big_data/zy/PRNet_tensorflow/training_data/InputImage --which_direction AtoB
		```
		
	- test on 111
		```
		docker pull vlsilab/zy_pix2pix:latest
		# make sure pull image sucessfully
		docker images
		# create container
		docker run -it --name zy_pix2pix_test --runtime=nvidia --ipc=host -v /srv:/srv -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=$DISPLAY --env QT_X11_NO_MITSHM=1 vlsilab/zy_pix2pix:latest
		# make sure create container sucessfully
		docker ps -a 
		# try trainin code
		CUDA_VISIBLE_DEVICES=0 python img2pos_mask_with_export_v2_depress_DAE_EBGAN_lr_decay0.8_v2_lr5e5_0326_pretrainD_fix2_aug_cer30_90_ns.py --mode train --checkpoint 102_train_model_mask_DAE_0310_lr_decay0.8_v2_lr5e5_pretrain_b32 --output_dir train_model_mask_DAE_EBGAN_0617_lr_decay0.8_v2_lr5e5_pretrainD_b32_fix2_aug_cer30_90_ns_test --max_epochs 300 --input_dir /srv/ssd1/zy/pix2pix-tensorflow-master/training_data/InputImage --which_direction AtoB
		```
<br>

## :large_orange_diamond: Existing enviroment

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
<br>

### Img2posGAN enviroment on work station 102
- Start and execute docker:
```
docker start zy_ pix2pix 
docker exec -it zy_pix2pix bash
# for both training and testing
cd /srv/big_data/zy/pix2pix-tensorflow-master
```
<br>

### Img2posGAN enviroment on work station 111
- Start and execute docker:
```
docker start zy_ pix2pix 
docker exec -it zy_pix2pix bash
# for both training and testing
cd /srv/ssd1/zy/pix2pix-tensorflow-master
```

## Supplement

### 102
- 打包自己的images上vlsilab docker hub
```
# 打包
docker commit container_id zy_prnet:latest
# 把要上傳到docker hub的image加上tag
docker tag zy_prnet:latest vlsilab/zy_prnet
# log in docker hub (vlsilab/vlsi95514)
docker login
# push image
docker push vlsilab/zy_prnet:latest
```

- Pull image to create containor
```
docker pull vlsilab/zy_prnet:latest
```


### 111
- 打包自己的images上vlsilab docker hub
```
# 打包
docker commit container_id zy_pix2pix_test:v1
# 把要上傳到docker hub的image加上tag
docker tag zy_pix2pix_test:v1 vlsilab/zy_pix2pix_final_test
# log in docker hub (vlsilab/vlsi95514)
docker login
# push image
docker push vlsilab/zy_pix2pix_final_test:latest
```

- Pull image to create containor
```
docker pull vlsilab/zy_pix2pix_final_test:latest
```