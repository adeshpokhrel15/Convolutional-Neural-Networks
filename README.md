# Convolutional-Neural-Networks
### 1. From Fully-Connected Layers to Convolutions </br>
### 2. Convolutions for Images
#### a. The Cross-Correlation Operation <br>
 An input tensor and a kernel tensor are combined to produce an output tensor through a cross-correlation operation.Note that along each axis, the output size is slightly smaller than the input size. Because the kernel has width and height greater than one, we can only properly compute the cross-correlation for locations where the kernel fits wholly within the image, the output size is given by the input size nh × nw minus the size of the convolution kernel kh × kw via <br>
            (nh − kh + 1) × (nw − kw + 1
#### b. Convolutional Layers <br>
A convolutional layer cross-correlates the input and kernel and adds a scalar bias to produce an output. The two parameters of a convolutional layer are the kernel and the scalar bias.
#### c. Object Edge Detection in Images <br>
#### d. Learning a Kernel <br>
We first construct a convolutional layer and initialize its kernel as a random tensor. Next, in each iteration, we will use the squared error to compare Y with the output of the convolutional layer. We can then calculate the gradient to update the kernel. For the sake of simplicity, in the following we use the built-in class for two-dimensional convolutional layers and ignore the bias. <br>

#### e. Cross-Correlation and Convolution <br>
Assuming that other conditions remain unchanged, when this layer performs strict convolution instead, the learned kernel K will be the same as K after K is flipped both horizontally and vertically. That is to say, when the convolutional layer performs strict convolution for the input and K the same output.Cross-correlation of the input and K will be obtained.

#### f. Feature Map and Receptive Field <br>
## Summary <br>
<li> The core computation of a two-dimensional convolutional layer is a two-dimensional crosscorrelation operation. In its simplest form, this performs a cross-correlation operation on the two-dimensional input data and the kernel, and then adds a bias.
<li> We can design a kernel to detect edges in images.
<li> We can learn the kernelʼs parameters from data.
<li> With kernels learned from data, the outputs of convolutional layers remain unaffected regardless of such layersʼ performed operations (either strict convolution or crosscorrelation).
<li> When any element in a feature map needs a larger receptive field to detect broader features on the input, a deeper network can be considered.
 
 ### 3. Padding and Stride <br>
 Padding can increase the height and width of the output. This is often used to give the output the same height and width as the input. The stride can reduce the resolution of the output, for example reducing the height and width of the output to only 1/n of the height and width of the input (n is an integer greater than 1).Padding and stride can be used to adjust the dimensionality of the data effectively
 
### 4. Multiple Input and Multiple Output Channels <br>
Multiple channels can be used to extend the model parameters of the convolutional layer. The 1 × 1 convolutional layer is equivalent to the fully-connected layer, when applied on a per pixel basis. The 1 × 1 convolutional layer is typically used to adjust the number of channels between network layers and to control model complexity.
 
### 5. Poling <br>
Taking the input elements in the pooling window, the maximum pooling operation assigns
the maximum value as the output and the average pooling operation assigns the average
value as the output. One of the major benefits of a pooling layer is to alleviate the excessive sensitivity of the
convolutional layer to location. We can specify the padding and stride for the pooling layer. Maximum pooling, combined with a stride larger than 1 can be used to reduce the spatial dimensions (e.g., width and height). The pooling layerʼs number of output channels is the same as the number of input channels.

### 6. LeNet <br> 


