# Convolutional-Neural-Networks
### 1. From Fully-Connected Layers to Convolutions </br>
### 2. Convolutions for Images
#### a. The Cross-Correlation Operation <br>
 An input tensor and a kernel tensor are combined to produce an output tensor through a cross-correlation operation.Note that along each axis, the output size is slightly smaller than the input size. Because the kernel has width and height greater than one, we can only properly compute the cross-correlation for locations where the kernel fits wholly within the image, the output size is given by the input size nh × nw minus the size of the convolution kernel kh × kw via <br>
            (nh − kh + 1) × (nw − kw + 1
#### b. Convolutional Layers <br>
A convolutional layer cross-correlates the input and kernel and adds a scalar bias to produce an output. The two parameters of a convolutional layer are the kernel and the scalar bias.


