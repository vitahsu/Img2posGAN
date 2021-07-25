Execution Example
===

- LCFD_ROOT = /path/to/LCFD

## Training

pretrained model training:
當初是在102train的 (batch32/300epoch)
CUDA_VISIBLE_DEVICES=0 python img2pos_mask_with_export_v2_depress_DAE_lr_decay0.8_v2_lr5e5_pretrain.py --mode train --output_dir train_model_mask_DAE_0310_lr_decay0.8_v2_lr5e5_pretrain_b32 --max_epochs 500 --input_dir /srv/big_data/zy/PRNet_tensorflow/training_data/InputImage --which_direction AtoB

img2pos_mask_with_export_v2_depress_DAE_lr_decay0.8_v2_lr5e5_pretrain.py
102_train_model_mask_DAE_0310_lr_decay0.8_v2_lr5e5_pretrain_b32









#### Basic
- Main file for training (LCFD_ROOT/train_lcfd.py)

```
cd LCFD_ROOT
python train_lcfd.py
```

- Default output path (LCFD_ROOT/logs/YYYYMMDDhhmm)

#### Configuration file
- Main file for configs (LCFD_ROOT/data/config.py)

#### Define the network
- Main file (LCFD_ROOT/lcfd.py)
- Modify the channels of each layer (find the below section in lcfd.py)

```
def build_lcfd(phase, num_classes=2):
    lcfd_cfg = [32, 'M', 48, 'M', 64, 'M', 64, 'M', 48, 'M', 48, 'M', 32]
    base_, head_ = multibox(lc_net(lcfd_cfg, 3), num_classes)   
    return LCFD(phase, base_, head_, num_classes)
```

#### Add additional predictors
- Main file (LCFD_ROOT/lcfd.py) and (LCFD_ROOT/config.py)
- Find the below sections in lcfd.py and config.py

```
# section 1 (lcfd.py)
# modify the layer index according to your requirement
def forward(self, x):
    # omit some code here

    for k in range(15):
        x = self.base_net[k](x)
    sources.append(x)

    for k in range(15, 19):
        x = self.base_net[k](x)
    sources.append(x)

    for k in range(19, 23):
        x = self.base_net[k](x)
    sources.append(x)

    for k in range(23, len(self.base_net)):
        x = self.base_net[k](x)
    sources.append(x)
```

```
# section 2 (lcfd.py)
# modify the layer index according to your requirement
def multibox(base_net, num_classes):
    loc_layers = []
    conf_layers = []
    net_source = [12, 16, 20, 24]

    for k, v in enumerate(net_source):
        # print(k, v)
        loc_layers += [nn.Conv2d(base_net[v].out_channels,
                                 4, kernel_size=3, padding=1)]
        conf_layers += [nn.Conv2d(base_net[v].out_channels,
                                  num_classes, kernel_size=3, padding=1)]

    return base_net, (loc_layers, conf_layers)
```

```
# section 3 (config.py)
# Find the below sections and modify according to your requirement
# The unit of the following numbers are pixels
_C.FEATURE_MAPS = [40, 20, 10, 5]
_C.STEPS = [8, 16, 32, 64]
_C.ANCHOR_SIZES = [32, 64, 128, 256]
```

#### Modify anchor size
- Main file (LCFD_ROOT/data/config.py)
- Find _C.ANCHOR_SIZES
- Modify the sizes according to your requirement
- The unit of size is pixel


## Inference

#### Basic
- Main file for inference (LCFD_ROOT/demo_lcfd.py)

```
cd LCFD_ROOT
python demo_lcfd.py
```

- Default input path (LCFD_ROOT/img)
- Default output path (LCFD_ROOT/tmp)


## Visualization
- Main file to plot the network (LCFD_ROOT/plot_lcfd.py)

```
cd LCFD_ROOT
python plot_lcfd.py
```

- Output 2 files in LCFD_ROOT
    - Digraph.gv
    - Digraph.gv.pdf


## Parameters count
- Main file to count parameters (LCFD_ROOT/params_count.py)

```
cd LCFD_ROOT
python params_count.py
```

- Output in terminal

## FLOPs count
- Main file to calculate FLOPs (LCFD_ROOT/flops_count.py)

```
cd LCFD_ROOT
python flops_count.py
```

- Output in terminal