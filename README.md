# Visual Manipulation Relationship Network
## Introduction
This package includes our latest proposed robotic grasping algorithms. Main framework is based on code of Faster RCNN (https://github.com/jwyang/faster-rcnn.pytorch).

Users for Pascal GPUs: you can skip the steps for building the C codes with Python because I have already done this.

Users for other GPUs: you have to follow the installation steps from https://github.com/jwyang/faster-rcnn.pytorch to make sure that the components of Faster-RCNN work fine.

## Installation
1. Follow https://github.com/jwyang/faster-rcnn.pytorch to make sure that Faster-RCNN works fine.
2. Run codes.

## Training Example
```bash
python main.py --dataset (DatasetName) --frame (AlgName) --net (BackboneName) --cuda
# like:
python main.py --dataset vmrdcompv1 --frame all_in_one --net res101 --cuda
```

## Testing
```bash
python main.py --test --dataset (DatasetName) --frame (AlgName) --net (BackboneName) --cuda --checkpoint (PointNum) --checkepoch (EpochNum) --GPU (GpuNum, Default:0)
#like:
python main.py --test --dataset vmrdcompv1 --frame all_in_one --net res101 --cuda --checkpoint 1000 --checkepoch 1 --GPU 0
```

## Performance

We want to re-implement the SOTA performance of the related algorithms. Some performance is shown below and it will be updated continuously.

*mAP*: mean Average Precision

*mAP-G*: mean Average Precision with Grasp Detection

*Rel-IA*: Image Accuracy of Relationship Detection

### Performance
Algorithm | Backbone | Training | Testing | mAP | mAP-G | Rel-IA
-|-|-|-|-|-|-
Faster R-CNN | ResNet-101 | VOC2007trainval | VOC2007test | 71.5 | - | -
FPN | ResNet-101 | VOC2007trainval | VOC2007test | 73.9 | - | -
ROI-GD | ResNet-101 | VMRDtrainval | VMRDtest | 94.5 | 75.7 | -

## Noteable Things
1. To train the network, you have to pre-download the pretrained models and put them in "data/pretrained_model" and name them the same as the usage in codes.
2. The training data should be placed or linked in "data".
3. The code will be improved continuously. Therefore, if you meet some problems, do not hesitate to contact me.
4. The included FPN and Focal Loss are uncompleted while Faster-RCNN and SSD can be used normally, though they are not the main contributions.

## Papers
1. Zhang, Hanbo, et al. "ROI-based Robotic Grasp Detection for Object Overlapping Scenes." arXiv preprint arXiv:1808.10313 (2018). To appear in IROS 2019.
2. Zhang, Hanbo, et al. "A Multi-task Convolutional Neural Network for Autonomous Robotic Grasping in Object Stacking Scenes." arXiv preprint arXiv:1809.07081 (2018). To appear in IROS 2019.
3. Zhang, Hanbo, et al. "Visual Manipulation Relationship Network for Autonomous Robotics." 2018 IEEE-RAS 18th International Conference on Humanoid Robots (Humanoids). IEEE, 2018.
4. Zhang, Hanbo, et al. "A Real-time Robotic Grasp Approach with Oriented Anchor Box." IEEE Transactions on Systems, Man and Cybernetics: Systems. Online Early Access.
5. Zhou, Xinwen, et al. "Fully convolutional grasp detection network with oriented anchor box." 2018 IEEE/RSJ International Conference on Intelligent Robots and Systems (IROS). IEEE, 2018.
6. Ren, Shaoqing, et al. "Faster r-cnn: Towards real-time object detection with region proposal networks." Advances in neural information processing systems. 2015.
7. Liu, Wei, et al. "Ssd: Single shot multibox detector." European conference on computer vision. Springer, Cham, 2016.
8. Lin, Tsung-Yi, et al. "Focal loss for dense object detection." Proceedings of the IEEE international conference on computer vision. 2017.

## Problem Shooting

1. [Solved] When setting batch_size of Faster RCNN to 1 and augmentation to True, we want to use SSD-like augmentation to generate more training data. However, it will cause NaN error.
2. There are some grasp and relation label errors in VMRD. However, we find that they do not affect the detection performance much. We will fix this problem as soon as possible.
3. This package only supports pytorch 0.4.0. When using 0.4.1, there will be segmentation fault (reason not found).
4. When training VMRN, the batchsize should be at least 2. Otherwise the network will not reach convergence.