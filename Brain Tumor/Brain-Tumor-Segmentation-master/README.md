
### Dataset
The [BraTS](http://www.med.upenn.edu/sbia/brats2018.html) data set is used for training and evaluating the model. This dataset contains four modalities for each individual brain, namely, T1, T1c (post-contrast T1), T2, and Flair which were skull-stripped, resampled and coregistered.

### Architecture
<br />

![image](https://github.com/Mehrdad-Noori/Brain-Tumor-Segmentation/blob/master/doc/model.jpg)

<br />

The network is based on U-Net architecture with some modifications as follows:
- The minor modifications: adding Residual Units, strided convolution, PReLU activation and Batch Normalization layers to the original U-Net
- The attention mechanism: employing [Squeeze and Excitation Block](https://arxiv.org/abs/1709.01507) (SE) on concatenated multi-level features. This technique prevents confusion for the model by weighting each of the channels adaptively 
<br />

<p align="left"><img src="https://github.com/Mehrdad-Noori/Brain-Tumor-Segmentation/blob/master/doc/attention.jpg" width="500" height="220"></p>

<br />

### Training Process
Since our proposed network is a 2D architecture, we need to extract 2D slices from 3D volumes of MRI images. To benefit from 3D contextual information of input images, we extract 2D slices from both Axial and Coronal views, and then train a network for each view separately. In the test time, we build the 3D output volume for each model by concatenating the 2D predicted maps. Finally, we fuse the two views by pixel-wise averaging.

<br />

<p align="left"><img src="https://github.com/Mehrdad-Noori/Brain-Tumor-Segmentation/blob/master/doc/MultiView.jpg" width="600" height="220"></p>

<br />


<br />

![image](https://github.com/Mehrdad-Noori/Brain-Tumor-Segmentation/blob/master/doc/example.jpg)

<br />

