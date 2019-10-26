## Image Corrrection GAN
This GAN was built as a part of internship hiring problem for [rephrase.ai](https://rephrase.ai).
The task was, given a set of degraded images, degraded using some unknown function, one has to
build a GAN to fix the images and bring them as closer to the ground truth as possible.

### Solution Implemented
To tackle this problem, I used a resnet like architecture in the generator and a VGG like architecture
as the discriminiator. And trained the model on a compound loss function consisting of pixelwise loss,
feature loss obtained using a pretrained VGG16 model, and finally the adversarial loss.

#### Generator Architecture
The generator is having a ResNet like architecture with skip connections of length 3. Each residual block
consists of 3 convoltion blocks activated using LeakyReLU.

### Discriminator Architecture
The discriminator network is having a VGG like architecture having Convolutions, Batch Norm activated with
LeakyReLU

### Loss Function Used

The loss function of the generator consists of a linear combination 3 losses.
- Pixelwise MSE with respect to the ground truth
- L1 Perceptual loss on features obtained from the last convolution of VGG16 model
- Adversarial component of the generator
![equation](https://latex.codecogs.com/gif.latex?Loss_%7BGenerator%7D%20%3D%20Loss_%7BPixelwise%7D%20+%20%5Cgamma%20%5Ccdot%20Loss_%7Bperceptual%7D%20+%20%5Ceta%20%5Ccdot%20Loss_%7Badversarial%7D)

**Evaluation Metric Used**: Peak signal to Noise Ratio (PSNR)

### Hyper Parameters used
For the following set of hyperparameters, Mean PSNR of **36.166** was achieved by the end of 10,000 steps

|Parameters|Value|
|--------------|-----|
|Image Patch Size| 128 x 128 |
|![residual_scaling](https://latex.codecogs.com/gif.latex?%5Calpha) (Residual Scaling)|0.1|
|![lrG](https://latex.codecogs.com/gif.latex?Learning%20Rate_%7BGenerator%7D)|0.0001|
|![lrD](https://latex.codecogs.com/gif.latex?Learning%20Rate_%7BDiscriminator%7D)|0.0004|
|![eta](https://latex.codecogs.com/gif.latex?%5Ceta)|![eta_value](https://latex.codecogs.com/gif.latex?10%5E%7B-3%7D)|
|![gamma](https://latex.codecogs.com/gif.latex?%5Cgamma)|0.7|HyperParameter|Value|


### Sample
From left to right: **Corrupted**, **Reconstructed**, **Original**
![sample](https://user-images.githubusercontent.com/13994201/67618552-92584600-f80e-11e9-9d2a-2e70fe0ec5b1.png)

