test on 102
docker pull vlsilab/zy_pix2pix:latest
docker images :確認有抓到image
docker run -it --gpus all --name zy_pix2pix_test --ipc=host -v /srv:/srv -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=$DISPLAY --env QT_X11_NO_MITSHM=1 vlsilab/zy_pix2pix:latest
docker ps -a :確認有創container成功
CUDA_VISIBLE_DEVICES=1 python img2pos_mask_with_export_v2_depress_DAE_EBGAN_lr_decay0.8_v2_lr5e5_0326_pretrainD_fix2_aug_cer10_45.py --mode train --checkpoint train_model_mask_DAE_0310_lr_decay0.8_v2_lr5e5_pretrain_b32 --output_dir 102_train_model_mask_DAE_EBGAN_0614_lr_decay0.8_v2_lr5e5_pretrainD_b32_fix2_aug_cer_cer10_45 --max_epochs 400 --input_dir /srv/big_data/zy/PRNet_tensorflow/training_data/InputImage --which_direction AtoB

測試完畢刪除container
docker stop container_id
docker rm container_id
docker rmi image_id

test on 111
docker run -it --name zy_pix2pix_test --runtime=nvidia --ipc=host -v /srv:/srv -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=$DISPLAY --env QT_X11_NO_MITSHM=1 vlsilab/zy_pix2pix:latest
docker ps -a :確認有創container成功
CUDA_VISIBLE_DEVICES=0 python img2pos_mask_with_export_v2_depress_DAE_EBGAN_lr_decay0.8_v2_lr5e5_0326_pretrainD_fix2_aug_cer30_90_ns.py --mode train --checkpoint 102_train_model_mask_DAE_0310_lr_decay0.8_v2_lr5e5_pretrain_b32 --output_dir train_model_mask_DAE_EBGAN_0617_lr_decay0.8_v2_lr5e5_pretrainD_b32_fix2_aug_cer30_90_ns_test --max_epochs 300 --input_dir /srv/ssd1/zy/pix2pix-tensorflow-master/training_data/InputImage --which_direction AtoB


python img2pos_run_basics_benchmark_batch_yaw_cropped_depress_angle.py
python img2pos_run_basics_benchmark_batch_yaw_cropped_show_depress.py

img2pos_run_basics_benchmark_batch_yaw_cropped_depress_angle.py
修改export_model_dir / error_report name / os.environ['CUDA_VISIBLE_DEVICES'] = '0'
output: error_report

img2pos_run_basics_benchmark_batch_yaw_cropped_show_depress.py
修改export_model_dir / save_folder / error_report name / os.environ['CUDA_VISIBLE_DEVICES'] = '0'
output: error_report and demo




- Run command line on work station
	- Train mode
```
CUDA_VISIBLE_DEVICES=0 python img2pos_mask_with_export_v2_depress_DAE_EBGAN_lr_decay0.8_v2_lr5e5_0326_pretrainD_fix2_aug_cer30_90_ns.py --mode train --checkpoint 102_train_model_mask_DAE_0310_lr_decay0.8_v2_lr5e5_pretrain_b32 --output_dir train_model_mask_DAE_EBGAN_0617_lr_decay0.8_v2_lr5e5_pretrainD_b32_fix2_aug_cer30_90_ns_test --max_epochs 300 --input_dir /srv/ssd1/zy/pix2pix-tensorflow-master/training_data/InputImage --which_direction AtoB
```
	- Export mode
```
CUDA_VISIBLE_DEVICES=0 python img2pos_mask_with_export_v2_depress_DAE_EBGAN_lr_decay0.8_v2_lr5e5_0326_pretrainD_fix2_aug_cer30_90_ns_export.py --mode export --output_dir export_train_model_mask_DAE_EBGAN_0610_lr_decay0.8_v2_lr5e5_pretrainD_b32_fix2_aug_cer30_90_ns_310_test --checkpoint train_model_mask_DAE_EBGAN_0617_lr_decay0.8_v2_lr5e5_pretrainD_b32_fix2_aug_cer30_90_ns
```
