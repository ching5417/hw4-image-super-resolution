# hw4-image-super-resolution
Code for NCTU Selected Topics in Visual Recognition using Deep Learning Homework 4

## Hardware
The following specs were used to create the original solution.
- Ubuntu 20.04 LTS
- Intel(R) Core(TM) i7-6700 CPU @ 3.40GHz (8 Cores)
- 1x NVIDIA GeForce GTX 1080

## Reproducing Submission
To reproduct the training and testing process, do the following steps:
1. [Installation](#installation)
2. [Training](#training)
3. [Make Submission](#make-submission)

## Installation
All requirements should be detailed in requirements.txt.
```
pip install -r requirement.txt
```

## Dataset Preparation
All required files are already in data directory. <br>
or <br>
you can use the original data and split it into training set / validation set <br>
Then, run augmentation.ipynb on your training set to generate more training data <br>
(augmentation: resize, crop, flip, rotation)

## Training

### Train models
To train models, run following commands.

```
$ cd EDSR_Tensorflow/
$ python main.py \
  --img \
  --train \
  --scale {upscaling factor} \
  --traindir {path/to/training/set/folder} \
  --validdir {path/to/validation/set/folder} \
  --export \
  --epochs {epoch number} \
  --batch {batch size} \
  --fromscratch
```
ex: `python main.py --train --scale 3 --traindir "../training_hr_images/" --validdir "../validation_hr_images/" --export --epochs 20 --batch 16 --fromscratch`

After training, the checkpoint will save to `/EDSR_Tensorflow/CKPT_dir/x3/` folder.
```
CKPT_dir/x3/
+- checkpoint
```

## Make Submission
Following command will upscale the test images with an upscaling factor of 3.
```
$ python main.py \
  --upscale \
  --scale {upscaling factor} \
  --image {path/to/testing/images/folder}
```
ex: ```python main.py --upscale --scale 3 --image "../testing_lr_images/"```

After testing, the upscaling images will output in `/EDSR_Tensorflow/images/` folder.

## Reference
https://github.com/Saafke/EDSR_Tensorflow
