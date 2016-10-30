
# Deep Convolutional Variational Autoencoder w/ Adversarial Network

A combination of the [DCGAN implementation](https://github.com/soumith/dcgan.torch) by soumith and the[variational autoencoder](https://github.com/Kaixhin/Autoencoders) by Kaixhin. Also used is the [KLD criterion](https://github.com/y0ast/VAE-Torch) by y0ast. Currently, the model is set up to upsample and downsample 128x128 color images; the code can, however, be easily modified to accept any number of different dimensions or color channel combinations. I may modify the script to allow for this to be automated, depending on the level of interest.  

I have added white noise to the original inputs that go through the discriminator after reading this [post on stabilizing GANS](http://www.inference.vc/instance-noise-a-trick-for-stabilising-gan-training/). Will post examples from training soon. 

## Prerequisites 
1. Torch7
2. CUDA
3. CUDNN
4. DPNN
5. Lua File System
6. optim
7. xlua

To run, simply execute the script using 

``` 
th daliVAE.lua -i [input folder destination] -o [output folder destination] -s [size of dataset (number of image files)] -c [destination for saving model checkpoints] -r [reconstructions folder]
```

where the input folder is expected to contain 128x128 color images. The model resamples the training set after every epoch so as to fit on a GPU and still (eventually) sample all of the training set. "Output" is for samples generated by the model, and "reconstructions folder" is to just save some reconstructions from the training set, to see how the VAE is doing. 

To run as a vanilla variational autoencoder, all you have to do is comment out any line that references "discriminator" and "netD", and the "optim.adam" functions in the main loop that reference "fDX" and "fGx". 
