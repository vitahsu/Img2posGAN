Extended Application Execution Example
===

## :large_orange_diamond: Resources

### Two resorces
- FaceProfilingRelease_v1.1 [3DFA](http://www.cbsr.ia.ac.cn/users/xiangyuzhu/projects/3DDFA/main.htm)
- CVPR2015_HPEN [HPEN](https://drive.google.com/file/d/1-hYpQy1EXZXiOUzlKikDjF8oaobB25iL/view)

### Data flow with background
- 首先將我們自己模型inference所偵測出的68點lanmark(僅取xy)利用notepad++轉換格式
- 並且放置在D:\CVPR2015_HPEN\High-Fidelity_PEN\Samples (img and keypoint.txt)
- 接著\zy_handover\3_Code\Extended_app\main_0_pretrained.m修改pts(landmark處複製貼上)
- 並且透過調整gamma_delta_an來改變角度 (line 149/150/289)

### Data flow without background
- zy_pix2pix 
	- /srv/ssd1/zy/face3d-master/examples/3_transform_.py
	- run command
		```
		python 3_transform_.py
		```

