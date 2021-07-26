PRNet Execution Example
===

## :large_orange_diamond: Training
- Modify training code including:
	- main_aug_rstce_xnor_281_cer3090.py: main training code
	- model_aug_rstce_xnor_281_cer3090.py: modify model architecture
	- augmentation_rstce_xnor_281_cer3090.py: adjust online data augmentation parameters
		- Trandforming (scale, rotation, translation)
		- Color channel scaling
		- Erasing
- Run command line on work station
```
python main_aug_rstce_xnor_281_cer3090.py
```


## :large_orange_diamond: Testing
- Modify testing code including:
	- api.py: modify model path
	- run_basics_benchmark_batch_yaw_cropped_angle.py: record angle(pitch/yaw/roll) of each images and inference for benchmark data and show performance
		- [nme2d, nme3d, landmark2d, landmark3d]: total mean error (2000/2000)
		- [0-30, 30-60, 60-90, mean]: 2D 68 landmark benchmark with different yaw range, mean is 3/3 
	- run_basics_benchmark_batch_yaw_cropped_show.py: show benchmark visualization results
		- pose, dense, mesh, ...
	- demo_inference.py: infernece for a new single 2D facial images
- Run command line on work station
```
python run_basics_benchmark_batch_yaw_cropped_angle.py
python run_basics_benchmark_batch_yaw_cropped_show.py
python demo_inference.py
```
