Code and Dataset
===

## :large_orange_diamond: Code setup
### PRNet
- Path to code (handover/3_Code/PRNet.zip)
	- training_code_PRNet_tensorflow
	- testing_PRNet-master
- Extract the files to your own workspace
- Details: PRNet official [github](https://github.com/YadiraF/PRNet) 

### Img2pos GAN
- Path to code (handover/3_Code/Img2posGAN.zip)
	- pix2pix-tensorflow-master
		- training
		- testing
- Extract the files to your own workspace
- Details: Pix2pixGAN tensorflow official [github](https://github.com/affinelayer/pix2pix-tensorflow) 

### Experimental results analysis
- Path to code (handover/3_Code/paper_analysis)
	- data_angle: angle of training dataset
	- draw_CED.py: paper figure
	- error_bar: comparison of models and do pose analysis and thesis figures
		- information in total_error_list_2Dkp is important!!!!!!!!!! 
	- run on pycharm in local PC
	
## :large_orange_diamond: Dataset setup
- Untar training_dataset.tar and benchmark_dataset.tar from handover/3_Code/Dataset/ to your desired path
	- training_dataset.tar: 300W-LP download from [3DFFA official website](http://www.cbsr.ia.ac.cn/users/xiangyuzhu/projects/3DDFA/main.htm)
		- angle_npy: pose including pitch, yaw, and roll in each data
		- InputImage: 2D facial images
		- LabelImage: visualized uv position map
		- LabelImage_npy: the data for training (because data have negative number)
	- benchmark_dataset.tar
		- AFLW2000_all: original dataset AFLW2000-3D download from [3DFFA official website](http://www.cbsr.ia.ac.cn/users/xiangyuzhu/projects/3DDFA/main.htm)
		- AFLW2000_all-crop: cropped information
		- AFLW2000_image_cropped: cropped images
- Details: How to transform 2D image and 3DMM parameter to uv position map?
	- please follow [here](https://github.com/YadiraF/face3d/blob/master/examples/8_generate_posmap_300WLP.py)
	- zy_pix2pix 
		- /srv/ssd1/zy/face3d-master/examples/8_generate_posmap_300WLP.py
		- run command
			```
			python 8_generate_posmap_300WLP.py
			```
