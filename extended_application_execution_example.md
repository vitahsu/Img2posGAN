Extended Application Execution Example
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
