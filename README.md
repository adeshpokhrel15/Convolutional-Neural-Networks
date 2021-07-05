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
LeNet, among the first published CNNs to capture wide attention
for its performance on computer vision tasks.. LeNet was eventually adapted to recognize digits for processing deposits in ATM machines. <br>
Two parts: <br> (i) a convolutional encoder consisting of
two convolutional layers; and <br>
 (ii) a dense block consisting of three fully-connected layers; <br>
 LeNetʼs dense block has three fully-connected layers, with 120, 84, and 10 outputs, respectively. Because we are still performing classification, the 10-dimensional output layer corresponds to the number of possible output classes.

### 7. AlexNet <br>
The first large-scale network deployed to beat conventional computer vision methods on a large-scale vision challenge.Objects in ImageNet data tend to occupy more pixels. Consequently, a larger convolution window is needed to capture the object.AlexNet changed the sigmoid activation function to a simpler ReLU activation function.AlexNet controls the model complexity of the fully-connected layer by dropout.To augment the data even further, the training loop of AlexNet added a great deal of image augmentation, such as flipping, clipping, and color changes.

### 8. Networks Using Blocks (VGG) <br>
 The basic building block of classic CNNs is a sequence of the following: <br> 
 (i) a convolutional layer with padding to maintain the resolution <br> 
 (ii) a nonlinearity such as a ReLU <br> 
 (iii) a pooling layer such as a maximum pooling layer <br> 
 VGG-11 constructs a network using reusable convolutional blocks. Different VGG models can
be defined by the differences in the number of convolutional layers and output channels in
each block.  The use of blocks leads to very compact representations of the network definition. It allows
for efficient design of complex networks.  In their VGG paper, Simonyan and Ziserman experimented with various architectures. In
particular, they found that several layers of deep and narrow convolutions (i.e., 3 × 3) were
more effective than fewer layers of wider convolutions.

### 9.  Network in Network (NiN) <br>
NiN were proposed based on a very simple insight: to use an MLP on the channels for each pixel separately. The idea behind NiN is to apply a fully-connected layer at each pixel location (for each height and width).  Each NiN block is followed by a maximum pooling layer with a stride of 2 and a window shape of  3×3 .NiN uses an NiN block with a number of output channels equal to the number of label classes, followed by a global average pooling layer, yielding a vector of logits. One advantage of NiN’s design is that it significantly reduces the number of required model parameters. However, in practice, this design sometimes requires increased model training time. NiN uses blocks consisting of a convolutional layer and multiple  1×1  convolutional layers. This can be used within the convolutional stack to allow for more per-pixel nonlinearity.
NiN removes the fully-connected layers and replaces them with global average pooling (i.e., summing over all locations) after reducing the number of channels to the desired number of outputs (e.g., 10 for Fashion-MNIST).Removing the fully-connected layers reduces overfitting. NiN has dramatically fewer parameters.The NiN design influenced many subsequent CNN designs.

### 10. Networks with Parallel Concatenations (GoogLeNet) <br>
 Here the outputs along each path are concatenated along the channel dimension and comprise the block’s output. The commonly-tuned hyperparameters of the Inception block are the number of output channels per layer. The details at different extents can be recognized efficiently by filters of different sizes. At the same time, we can allocate different amounts of parameters for different filters.The GoogLeNet model is computationally complex, so it is not as easy to modify the number of channels as in VGG.The Inception block is equivalent to a subnetwork with four paths. It extracts information in parallel through convolutional layers of different window shapes and maximum pooling layers.  1×1  convolutions reduce channel dimensionality on a per-pixel level. Maximum pooling reduces the resolution. GoogLeNet connects multiple well-designed Inception blocks with other layers in series. The ratio of the number of channels assigned in the Inception block is obtained through a large number of experiments on the ImageNet dataset. GoogLeNet, as well as its succeeding versions, was one of the most efficient models on ImageNet, providing similar test accuracy with lower computational complexity.
 
### 11. Batch Normalization <br>



