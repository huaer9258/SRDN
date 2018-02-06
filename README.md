<<<<<<< HEAD
# torch-srgan

**This code only provides the implementation of SRResNet. SRGAN is implemented but the result is not very good.**

Torch implementation of [Photo-Realistic Single Image Super-Resolution Using a Generative Adversarial Network](https://arxiv.org/abs/1609.04802) that generates high-resolution images from low-resolution input images, for example:

<img src="docs/comic_mse.png" width="900px"/>

## Setup

### Prerequisites
- Linux
- NVIDIA GPU + CUDA CuDNN
- Python with Numpy, Scipy, PIL, h5py
- Torch with nn, image, graphicsmagick, trepl, hdf5, cunn, cutorch

## Getting Started
- Clone this repo:
```bash
git clone https://github.com/huangzehao/torch-srgan
cd torch-srgan
```
### Train
- Download [imagenet valset](http://image-net.org/download-images) for training

- Prepare training data
```bash
python make_data.py --train_dir $(train_data_folder) --val_dir $(val_data_folder) --output_file $(output_hdf5_file)
```
- (Optional) Download VGG19 model for perceptual training
```bash
cd models
bash VGG19.sh
```
- Train the model
```bash
mkdir checkpoint val
# SRResNet MSE
CUDA_VISIBLE_DEVICES=0 th train.lua -h5_file $(output_hdf5_file) -num_epoch 50 -loss 'pixel'
# SRResNet MSE VGG22 (need VGG19 model)
CUDA_VISIBLE_DEVICES=0 th train.lua -h5_file $(output_hdf5_file) -num_epoch 50 -loss 'percep' -percep_layer 'conv2_2' -use_tanh
# SRResNet MSE VGG54 (need VGG19 model)
CUDA_VISIBLE_DEVICES=0 th train.lua -h5_file $(output_hdf5_file) -num_epoch 50 -loss 'percep' -percep_layer 'conv5_4' -use_tanh
```
### Test
- Test trained model
```bash
# SRResNet MSE
CUDA_VISIBLE_DEVICES=0 th test.lua -img ./imgs/comic_input.bmp -output ./output.bmp -model ./models/SRResNet_MSE_100.t7
# SRResNet MSE VGG22
CUDA_VISIBLE_DEVICES=0 th test.lua -img ./imgs/comic_input.bmp -output ./output.bmp -model ./models/SRResNet_MSE_VGG22_100.t7 -use_tanh
# SRResNet MSE VGG54
CUDA_VISIBLE_DEVICES=0 th test.lua -img ./imgs/comic_input.bmp -output ./output.bmp -model ./models/SRResNet_MSE_VGG54_100.t7 -use_tanh
```

## Acknowledgments
Code borrows heavily from [fast-neural-style](https://github.com/jcjohnson/fast-neural-style) and [cifar.torch](https://github.com/szagoruyko/cifar.torch). Thanks for their excellent work!
=======
# SRDN
Implementation codes of SRDN
>>>>>>> 32fadd83f0e8d9fb939006619e7e95fada55d6a3
