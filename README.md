# Research_iNESlab
This repository contains my contributions in my lab, which has essential and important projects to take a good start in deep world.
# 1.1) DarkNet Implimentation on our own dataset on gpu.
# Setp 1: Comfirmation
First install DarkNet from the offical website https://pjreddie.com/darknet/install/ .

Before this step you have to make sure that your system must have navidia gpu support and opencv running in it for better results.
Install darket in your ubuntu machine server with modification in makefile such as

GPU=1;

OpenCv=1;
# Step 2: Data Collection
Collect the data on which we want to train over network and images size is not an issue according to our experiences because we trained yolo_2 on 720*1280 resolution.
# Step 3: Labeling Tool for annotation of data.
By long research, we found an annotattion tool to label our data and we made some modification in it related to crosspounding sequences of images. I also upload my modified code with the name annotation.py and attaching complete guide to use it.
# Step 4: Editing in obj.cfg, obj.data, obj.names files.
After labeling, we have to make some changes cfg file in the cfg directory in darknet and for doing this we have to choose our model. For example, for tiny-yolo.cfg, make copy and rename it as we like i.e) yolo-obj.cfg, then open and edit it.

line 125, classes=2

line 119, filter=35     # filters=(classes + 5)*5

we will create data file and place it the data directory. The obj.data file look like this:   

obj.data/

classes= 2

train  = data/train.txt

valid  = data/test.txt

names = data/obj.names

backup = backup

results= results

Now, create obj.names file in data directory which have the name of classes according to labeling sequence.

names.obj/

car

back_side
# Step 5: Path generation code for test and train datasets regarding to darknet.
You need to run the train_test_prep.py file in the same directory which contains your dataset.
The resulting txt files have the full path of data with respect to darknet.
# Step 6: Placing train.txt, test.txt, obj.data, obj.names, dataset and labels.
Please place train.txt, test.txt, obj.data, obj.names, dataset,and labels in data directory of darket.
Before this please make sure that our images and crosspounding labels must be in same directory.
# Step 7: Download the weights of pretrained model
Please download darknet19_448.conv.23 file and place in darkNet's directory.
https://github.com/KleinYuan/easy-yolo/blob/master/darknet19_448.conv.23
# Step 8: Open your terminal and start training and testing the models
1) To Start Training:

./darknet detector train cfg/obj.data cfg/yolo-obj.cfg darknet19_448.conv.23

2) To testing

./darknet detector test cfg/obj.data cfg/yolo-obj.cfg yolo-obj.weights

3) To apply our model to validates on videos

./darknet detector demo data/obj.data cfg/yolo-obj.cfg yolo-obj.weights video_name.file_format -i 0
