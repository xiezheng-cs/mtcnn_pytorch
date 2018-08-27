
# 人脸检测


---
## 实验目的
1. 理解和掌握基于神经网络的人脸检测方法的理论基础知识。
2. 理解[MTCNN](https://kpzhang93.github.io/MTCNN_face_detection_alignment/paper/spl.pdf)人脸检测的基本流程，并加以实践。


## 训练数据集
为了训练PNet和RNet，将[WiderFace](http://mmlab.ie.cuhk.edu.hk/projects/WIDERFace/)用于人脸分类和人脸边界框回归；为了训练ONet，将[WiderFace](http://mmlab.ie.cuhk.edu.hk/projects/WIDERFace/)用于人脸分类和人脸边界框回归，使用[Training Dataset](http://mmlab.ie.cuhk.edu.hk/archive/CNN_FacePoint.htm)用于人脸特征点回归。


## 实验环境
[anaconda3](https://www.anaconda.com/download/)
[pytorch 0.4.1](https://pytorch.org/)
[torchvision](https://pytorch.org/)
[opencv-python](https://pypi.org/project/opencv-python/)等。


## 实验时间及地点
2018年7月28日 晚上7:00-9:00 B7-138


## 实验步骤
**一、获取代码**

实验完整代码[mtcnn_pytorch](https://github.com/xiezheng-cs/mtcnn_pytorch)，可直接下载或是通过git clone命令下载。
```bash
git clone https://github.com/xiezheng-cs/mtcnn_pytorch.git
```

**二、实验环境安装**
1. 确保本机或是服务器已安装好[anaconda3](https://www.anaconda.com/download/)环境；
2. pip或conda安装[pytorch 0.4.1 和 torchvision](https://pytorch.org/)环境；
3. pip或conda安装[opencv-python](https://pypi.org/project/opencv-python/)环境。

```bash
pip install http://download.pytorch.org/whl/cpu/torch-0.4.1-cp36-cp36m-win_amd64.whl     # Windows
pip install http://download.pytorch.org/whl/cpu/torch-0.4.1-cp36-cp36m-linux_x86_64.whl  # Linux
pip install torchvision
pip install opencv-python
```

**三、简单测试给定模型**

直接使用我们[训练好的网络模型](https://github.com/xiezheng-cs/mtcnn_pytorch/releases)在给定的测试数据集(位于mtcnn_pytorch/data/test_images/目录下,共64张测试图片)，运行以下命令，即可在mtcnn_pytorch/data/you_result/目录下查看检测结果。
```bash
cd mtcnn_pytorch/
python test_image.py
```

**四、训练**

**注意：** 在训练过程中，需要注意训练数据集路径是否与你本机或服务器存放路径一致，若不一致，则需修改相关文件代码。

1.训练PNet网络
```bash
cd mtcnn_pytorch
python preprocessing/gen_pnet_data.py
python preprocessing/assemble_pnet_imglist.py
python training/pnet/train.py
```


2.训练RNet网络

```bash
cd mtcnn_pytorch
python preprocessing/gen_rnet_data.py
python preprocessing/assemble_rnet_imglist.py
python training/rnet/train.py
```


3.训练ONet网络

```bash
cd mtcnn_pytorch
python preprocessing/gen_landmark_48.py
python preprocessing/gen_onet_data.py
python preprocessing/assemble_onet_imglist.py
python training/onet/train.py
```
训练完成，即可在mtcnn_pytorch/results/目录下得到三个训练好的网络模型。

**五、简单测试自己训练好的模型**

在给定的测试数据集(位于mtcnn_pytorch/data/test_images/目录下,共64张测试图片)简单测试自己训练好的网络模型，运行以下命令，即可在mtcnn_pytorch/data/you_result/目录下查看检测结果。
```
cd mtcnn_pytorch/
python test_youModel_images.py
```

**注意：** 检查测试文件test_youModel_images.py中的模型路径是否与你训练好的模型路径一致，若不一致，则修改路径。


**六、可在FDDB上测试训练好的模型**

-----
