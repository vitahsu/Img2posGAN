Environment Setup
===

## Basic idea requirements
- Reference slides (zy_handover/2_Meeting_slides/Tutorial/ciw_docker_environment.pptx)

### Hardware

- Nvidia GPU available

```
nvidia-smi
```

## Create nwe enviroment

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
- Start and execuvate docker:
```
docker start zy_prnet_tb_gpu2
docker exec -it zy_prnet_tb_gpu2 bash
# for training
cd /srv/big_data/zy/PRNet_tensorflow
# for testing
cd /srv/big_data/zy/PRNet-master
```

### Img2posGAN enviroment on work station 111
- Start and execuvate docker:
```
docker start zy_ pix2pix 
docker exec -it zy_pix2pix bash
# for both training and testing
cd /srv/ssd1/zy/pix2pix-tensorflow-master
```


