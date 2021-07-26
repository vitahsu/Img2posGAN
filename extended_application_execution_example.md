Extended Application Execution Example
===

## Resources
使用兩包online open resource(D:\FaceProfilingRelease_v1.1)(D:\CVPR2015_HPEN)
首先將我們自己模型所偵測出的68點lanmark利用notepad++轉換格式
並且放置在D:\CVPR2015_HPEN\High-Fidelity_PEN\Samples
接著仿造D:\CVPR2015_HPEN\High-Fidelity_PEN\main_0_pretrained.m修改pts(landmark處複製貼上)
接著將程式debug斷點設在143行執行以取得f, phi, gamma, theta, t3d, alpha, alpha_exp

接著仿造D:\FaceProfilingRelease_v1.1\main_0_pretrained.m以複製貼上方式修改剛剛取得的f, phi, gamma, theta, t3d, alpha, alpha_exp參數
並且透過調整gamma_delta_an來改變角度

102
zy_pix2pix
/srv/big_data/zy/face3d-master/examples/3_transform_.py
(F:\face3d-master\examples)