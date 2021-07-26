PRNet Execution Example
===

## :large_orange_diamond: Training
- Modify training code including:
	- main_aug_rstce_xnor_281_cer3090.py: main training code
	- model_aug_rstce_xnor_281_cer3090.py: modify model architecture
		- modify save_path
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
	- predictor.py: imported by api.py
	- api.py: imported by run_basics_benchmark_batch_yaw_cropped_angle.py, run_basics_benchmark_batch_yaw_cropped_show.py and demo_inference.py to modify model path (prn_path)
	- run_basics_benchmark_batch_yaw_cropped_angle.py: record angle(pitch/yaw/roll) of each images and inference for benchmark data and show performance
		- modify error_report name / os.environ['CUDA_VISIBLE_DEVICES'] = '0'
		- output: performance and error_report
			- [nme2d, nme3d, landmark2d, landmark3d]: total mean error (2000/2000)
			- [0-30, 30-60, 60-90, mean]: 2D 68 landmark benchmark with different yaw range, mean is 3/3 
		- Run command
			```
			python run_basics_benchmark_batch_yaw_cropped_angle.py
			```
	- run_basics_benchmark_batch_yaw_cropped_show.py: show benchmark visualization results
		- modify save_folder / error_report name / os.environ['CUDA_VISIBLE_DEVICES'] = '0'
		- output: performance, error_report and demo
		- Run command
			```
			python run_basics_benchmark_batch_yaw_cropped_show.py
			```
			
	- demo_inference.py: infernece for a new single 2D facial images
		- modify inputDir, outputDir ...
		- Run command
			```
			python demo_inference.py
			```