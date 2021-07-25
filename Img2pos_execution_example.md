Img2pos GAN Execution Example
===

## Training
- Modify training code including:
	- img2pos_aug_cer30_90_ns.py: main training code
	- img2pos_aug_cer30_90_ns_export.py: export model
	- augmentation_rstce_xnor_281_cer30_90_ns.py: adjust online data augmentation parameters
		- Trandforming (scale, rotation, translation)
		- Color channel scaling
		- Erasing
- Run command line on work station
```
python img2pos_aug_cer30_90_ns.py
```

- Pretrained discriminator model:
	- Existing model trained on 102 (batch32/300epoch)
		- img2pos_mask_with_export_v2_depress_DAE_lr_decay0.8_v2_lr5e5_pretrain.py: training code
		- 102_train_model_mask_DAE_0310_lr_decay0.8_v2_lr5e5_pretrain_b32: model
```
CUDA_VISIBLE_DEVICES=0 python img2pos_mask_with_export_v2_depress_DAE_lr_decay0.8_v2_lr5e5_pretrain.py --mode train --output_dir train_model_mask_DAE_0310_lr_decay0.8_v2_lr5e5_pretrain_b32 --max_epochs 500 --input_dir /srv/big_data/zy/PRNet_tensorflow/training_data/InputImage --which_direction AtoB
```

## Testing
- Modify testing code including:
	- img2pos_run_basics_benchmark_batch_yaw_cropped_depress_angle.py: record angle(pitch/yaw/roll) of each images and inference for benchmark data and show performance
		- [nme2d, nme3d, landmark2d, landmark3d]: total mean error (2000/2000)
		- [0-30, 30-60, 60-90, mean]: 2D 68 landmark benchmark with different yaw range, mean is 3/3 
	- img2pos_run_basics_benchmark_batch_yaw_cropped_show_depress.py: show benchmark visualization results
		- pose, dense, mesh, ...
	- img2pos_demo_cropped_show.py: infernece for a new single 2D facial images
		- Prepare test_input(original image) to run on zy_PRNet img2pos_demo_cropped.py and img2pos_api_cropped.py to get the test_input_cropped(cropped images) and test_tform(record pose in .txt to help recover back to space of original image),
		  then copy three file(test_input/test_input_cropped/test_tform_txt) to zy_pix2pix and run img2pos_demo_cropped_show.py on zy_pix2pix for inference
		
- Run command line on work station zy_pix2pix
```
python img2pos_run_basics_benchmark_batch_yaw_cropped_depress_angle.py
python img2pos_run_basics_benchmark_batch_yaw_cropped_show_depress.py
python img2pos_demo_cropped_show.py
```
- Run command line on work station zy_PRNet
```
python img2pos_demo_cropped.py

```