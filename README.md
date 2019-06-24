# Autoencoder-basic-image-compression

A basic implementation of Convolutional Autoencoder for image compression on MNIST dataset.

## Motivation

JPEG compression is currently the industry standard for image compression, however, there are many ways that Auto-encoders are being expanded in research that could push auto-encoder data compression over JPEG. This mini-project tries to achieve good results on mnist dataset.

## Tech/FrameWork Used

Python 3.7.3

Keras with tensorflow as Backend

# Implementation Details

The autoencoder model consist of 

### 1. Encoder
Three convolutional layers followed by max pooling, reducing the kernel size by half after evry convolution. Three such units were used
```ruby
x = Conv2D(256, (3, 3), activation='relu', padding='same')(input_img)
x = Conv2D(128, (3, 3), activation='relu', padding='same')(x)
x = Conv2D(64, (3, 3), activation='relu', padding='same')(x)
x = MaxPooling2D(pool_size=(2, 2))(x)
x = Conv2D(32, (3, 3), activation='relu', padding='same')(x)
x = Conv2D(16, (3, 3), activation='relu', padding='same')(x)
x = Conv2D(8, (1, 1), activation='relu', padding='same')(x)
x = MaxPooling2D(pool_size=(2, 2))(x)
x = Conv2D(4, (3, 3), activation='relu', padding='same')(x)
x = Conv2D(2, (1, 1), activation='relu', padding='same')(x)
x = Conv2D(1, (1, 1), activation='relu', padding='same')(x)
```
### 2. Decoder
Similar to Encoder in opposite direction only instead of max pooling upscaling was used.(Transpose Convolution was not used due to Hardware Bottleneck and minimal difference)
```ruby
x = Conv2D(2, (1, 1), activation='relu', padding='same')(x)
x = Conv2D(4, (3, 3), activation='relu', padding='same')(x)
x = Conv2D(8, (3, 3), activation='relu', padding='same')(x)
x = UpSampling2D((2, 2))(x)
x = Conv2D(16, (3, 3), activation='relu', padding='same')(x)
x = Conv2D(32, (3, 3), activation='relu', padding='same')(x)
x = Conv2D(64, (3, 3), activation='relu', padding='same')(x)
x = UpSampling2D((2, 2))(x)
x = Conv2D(128, (3, 3), activation='relu', padding='same')(x)
x = Conv2D(256, (3, 3), activation='relu', padding='same')(x)
x = Conv2D(1, (3, 3), activation='tanh', padding='same')(x)
```
# Results

The original MNIST image size is 28 x 28 (Grayscale) but using an encoder the feature space was reduced to 7 x 7.
Thus 28 x 28 = 784 was reduced to mere 7 x 7 = 49 pixels.<br />
The Left Column is of original images and right is of autoencoder based images
![alt text](https://github.com/Arnav0400/Autoencoder-basic-image-compression/blob/master/Results.jpg)

# License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

