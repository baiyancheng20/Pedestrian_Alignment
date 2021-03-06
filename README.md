# Pedestrian Alignment Network for Person Re-identification

This repo is for our arXiv paper (https://arxiv.org/abs/1707.00408). 
The main idea is to align the pedestrian within the bboxes, and reduce the noisy factors i.e., scale and pose variances.

## Network Structure
![](https://github.com/layumi/Pedestrian_Alignment/blob/master/fig2.jpg)
For more details, you can see this [png file](https://raw.githubusercontent.com/layumi/Pedestrian_Alignment/master/PAN.png). But it is low-solution now, and I may replace it recently.

## Installation
1.Clone this repo.

	git clone https://github.com/layumi/Pedestrian_Alignment.git
	cd Pedestrian_Alignment
	mkdir data

2.Download the pretrained model. Put it into './data'.

	cd data
	wget http://www.vlfeat.org/matconvnet/models/imagenet-resnet-50-dag.mat
	
3.Compile Matconvnet
**(Note that I have included my Matconvnet in this repo, so you do not need to download it again.)**

You just need to uncomment and modify some lines in `gpu_compile.m` and run it in Matlab. Try it~
If you fail in compilation, you may refer to http://www.vlfeat.org/matconvnet/install/
    
## Dataset
Download [Market1501 Dataset] (http://www.liangzheng.org/Project/project_reid.html)

## Train
1. Add your dataset path into `prepare_data.m` and run it. Make sure the code outputs the right image path.

2. Run `train_id_net_res_market_new.m` to pretrain the base branch.

3. Run `train_id_net_res_market_align.m` to finetune the whole net.

## Test
1. Run `test/test_gallery_query_base.m` and `test/test_gallery_query_align.m` to extract the image features from base brach and alignment brach. Note that you need to change the dir path in the code. They will store in a .mat file. Then you can use it to do evaluation.

2. Evaluate feature on the Market-1501. Run `evaluation/zzd_evaluation_res_faster.m`. You can get the following Single-query Result.

| Methods               | Rank@1 | mAP    | 
| --------              | -----  | ----   | 
| Ours           | 82.81% | 63.35% | 

## Visualize Results
We conduct an extra interesting experiment:
**When zooming in the input image (adding scale variance), how do our alignment network react?**

We can observe a robust transform on the output image (focusing on the human body and keeping the scale).

The left image is the input; The right image is the output of our network.

![](https://github.com/layumi/Person_re-ID_stn/blob/master/gif/0018_c4s1_002351_02_zoomin.gif)
    ![](https://github.com/layumi/Person_re-ID_stn/blob/master/gif/0153_c4s1_026076_03_zoomin.gif)
    ![](https://github.com/layumi/Pedestrian_Alignment/blob/master/gif/0520_c4s3_001373_03_zoomin.gif)


![](https://github.com/layumi/Pedestrian_Alignment/blob/master/gif/0520_c5s1_143995_06_zoomin.gif)
    ![](https://github.com/layumi/Pedestrian_Alignment/blob/master/gif/0345_c6s1_079326_07_zoomin.gif)
    ![](https://github.com/layumi/Pedestrian_Alignment/blob/master/gif/0153_c4s1_025451_01_zoomin.gif)
