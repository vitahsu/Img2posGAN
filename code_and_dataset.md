Code and Dataset
===

## Code setup
- Path to code (handover/3_Code/LCFD.zip)
- Extract the files to your own workspace
- The above path (/path/to/LCFD) is noted as LCFD_ROOT in the following document

## Dataset setup
- (option1) Download WIDERFACE dataset from [official website](http://shuoyang1213.me/WIDERFACE/)
- (option2) Copy from (handover/3_Code/dataset/wider_ws)
- Extract or copy WIDERFACE dataset to your desired path

#### Prepare lists for training and validation
- Modify paths in (LCFD_ROOT/data/config.py)
    - _C.FACE.WIDER_DIR = /path/to/WIDER_face
- Run (LCFD_ROOT/prepare_wider_data.py)

```
cd LCFD_ROOT
python prepare_wider_data.py
```

- 2 files generated in (LCFD_ROOT/data/)
    - face_train.txt
    - face_val.txt
