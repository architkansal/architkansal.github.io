---
layout: post
title: Discriminatory Scatternet Framework For Object Classification
---

<link rel="stylesheet" type="text/css" href="{{ site.baseurl }}/post.css" />
In this article, I am going to talk about my UG thesis project. I have been pursuing ML since the 2nd year of college. I have taken several introductory and advanced courses, participated in online contests and organized workshops & contests for college fests. So, I decided to work on some ML problem as part of my thesis as well.

I collaborated with [Amarjot Singh](https://www.linkedin.com/in/amarjot-singh-b5269815/) and [Prof. K. V. Kadambari](https://www.nitw.ac.in/faculty/id/16335/) and we decided to work on scattering networks. ScatterNets are a type of hand-engineered networks in computer vision.
Now, let me quickly introduce the problem domain.

## Introduction

Object classification is the task of classifying images by extracting features from image data.
The fundamental challenge for any such system lies within the simultaneous requirement of the capacity to distinguish between similar looking image regions while being invariant to appearance-altering transformations.

Despite the success of the deep networks(CNNs) in the domain, there remains a fundamental lack of
understanding in the design and optimization of these networks which makes it difficult
to develop them. Also, training of these networks require large labeled datasets which in
numerous applications may not be available.

In this work, we propose a hybrid semi-supervised architecture comprising of
a manifold separation technique and ScatterNet for Image Classification. The prime motivation behind this work is introducing a way to provide discrimination between object of interest and background noise for the scatternets.

## Network Architecture 

There are two parts of the system. Lets take a look at each of them separately.

In the first stage, we learn templates for each object class which will be used later for separating the foreground object of interest and background clutter.

In the second stage of the network, a two-layer DTCWT scatternet is used. We filter the input at first layer of scatternet, then we apply manifold separation on the output of first layer using the templates learned in previous stage and further pass the filtered foreground and background manifolds to the second layer of scatternet. Finally, we merge the two manifolds after filtering them in the second layer. And the output from both the first layer and merged manifolds are passed to support vector machine for classification.

Illustration below shows the input image (x) of size 112 × 112. Image representations
at m = 1 layer (first layer) are obtained using DTCWT filters at 4 scales and 6 orientations. Next the Manifold
separation using deformed templates is carried out and the foreground and background
manifolds are, separately, further passed through m = 2 layer (second layer) (In the second layer, each of the 6 orientations are further filtered at each scale upto the coarsest scale as shown the the diagram, e.g. for j=1 in first layer we have 112x112x6 as output so in the second layer each of six 112x112 is used to get 56x56x6, 28x28x6, 14x14x6 because the coarsest scale in the first layer is 14x14) and then merged to obtain
the final representations.

![Complete Network Architecture]({{site.baseurl}}/images/scatternet/dscatternet2.png "Network Architecture")

## Stage 1 : Unsupervised Template Learning Using Active Basis Model(ABM)

In this stage, we feed the input image to an ABM which performs unsupervised
template learning for foreground object using shared sketch algorithm. The algorithm works
separately on each input class. The gabor wavelets are used for learning object templates.
It stores the common templates for each class as well as the templates which are locally
adjusted (called **deformed templates**) corresponding to each training image.
The below image is illustration of an active basis model.
![Active Basis Model Architecture]({{site.baseurl}}/images/scatternet/activebasis.jpg "Active Basis Model Architecture")

The figure below shows the templates learnt for caltech-101
dataset using 30 training images for each class. The input image resolution is 112x112.
The classes are Buddha, Lamp, Okapi and Starfish from left to right.

![Common Templates]({{site.baseurl}}/images/scatternet/common-templates.png "Common Templates")

The figure below shows the deformed templates learnt for
caltech-101 dataset corresponding to one specific training images for two classes. The input
image resolution is 112x112. The classes are Buddha and Face from left to right.

![Deformed Templates]({{site.baseurl}}/images/scatternet/deformed-templates.png "Deformed Templates")

## Stage 2 : Discriminatory Scattering Network

This section details the hand-crafted scattering network termed as, the Discriminatory
Scattering Network that extracts relatively symmetric translation invariant feature representations from the input signal. We use a DTCWT Scatternet which is a parametric log based improved numerous version of the multi-layer hand-crafted Scattering Networks. Translation invariant features are extracted by the Scatternet using the dual-tree complex
wavelet transform (DTCWT).

The scatternet consists of two layers. At the first layer, the input signal x
is filtered with dual-tree complex wavelets at multiple scales(4) and pre-defined orientations (6) to obtain invariant features. Further, Cascaded wavelet filtering is performed at the second layer separately for foreground object of interest and background clutter that retrieves the high frequency components lost due to smoothing.

In the image below, the first row shows the input images. 2nd row is the corresponding 2nd layer
layer output for scatternet without manifold separation. The 3rd row is the output of 2nd layer layer for Discriminatory scatternet(with manifold separation). It can clearly be observed that feature space obtained with manifold separation technique is much better suited for classsification by SVM than the feature space obtained without it.

![L2 Output]({{site.baseurl}}/images/scatternet/l2.png "L2 Output")

The coefficients extracted from each layer are concatenated to generate a feature vector
for each of the images in the training dataset. The scattering feature vectors are then
normalized across each dimension and then passed to G-SVM for classification as shown in the figure below.

![Complete Network Architecture]({{site.baseurl}}/images/scatternet/dscatternet2.png "Network Architecture")

**NOTE** : *The merging the foreground and background manifolds is required
because the manifold separation is not always perfect and parts of foreground might be
present in the background manifold which might be required for the classification task
performed by the SVM. This is also verified experimentally by running classification only
using foreground manifold and compared those results with feature space obtained by
merging the two manifolds. The merged-manifold space gave better classification accuracy
compared to space only containing the foreground manifold.*

##  Manifold Separation Techniques 

This section details the two techniques engineered to discriminate between object of interest
and background clutter using the deformed template learned by ABM. Manifold Separation is applied on the output of first layer of scatternet and two manifolds thus obtained are then separately passed to second layer of the scatternet. 

## Manifold separation using rectangular-intersection technique

In this technique, a rectangular box is drawn around the deformed template (obtained by ABM corresponding to each image for training data. For the test data, the template matching is performed for each object class using the *common template* and the one that gives highest matching score is used to obtain deformed template)
using the left-most, right-most and top-most and bottom-most non-zero pixel values in the deformed
template. The deformed template is also dilated using a relatively large structuring element ( [Image Dilation](https://www.mathworks.com/help/images/ref/imdilate.html) )
followed by hole-filling operation ([Filling Image Holes](https://www.mathworks.com/help/images/ref/imfill.html)). And then only the pixel values where both the rectangular
box and the dilated-filled template have non-zero pixel values are taken to obtain the foreground object of interest.

Below image depicts rectangular-intersection based manifold separation
technique where each row (from left to right) consists of input image, Layer1 output for
a specific orientation, deformed template, dilated deformed template, dilated-hole-filled deformed template, rectangualar box, intersection of
rectangular template with dilated-hole-filled version and finally the extracted foreground object of
interest for the corresponding input image.

![Rectangular Manifold Separation]({{site.baseurl}}/images/scatternet/grid_rect_2.png "Rectangular Manifold Separation")

## Manifold separation using dilation-erosion technique

Here, the deformed template obtained for the object of interest ( obtained by ABM corresponding to each image for training data. For the test data, the template matching is performed for each object class using the *common template* and the one that gives highest matching score is used to obtain deformed template) is first dilated [Image Dilation](https://www.mathworks.com/help/images/ref/imdilate.html) ) followed by
hole-filling operation ([Filling Image Holes](https://www.mathworks.com/help/images/ref/imfill.html)) and finally it is eroded ([Image Erosion](https://www.mathworks.com/help/images/ref/imerode.html))to avoid including unnecessary clutter from
background. The structuring elements and their values are set heuristically for both dilation
and erosion operations.

Below image depicts dilation-erosion based manifold separation technique on a deformed template displayed in the first row. In second row, each of the columns (from top to bottom) consists of dilated version of template followed by hole-filled version of dilated template followed by eroded version of the dilated-hole-filled template
which are finally used to extract foreground objects of interest as displayed in the last row. 
The structuring element used for dilation and erosion operation are different for each column. This signifies the effect of choosing the correct structing element and its impact on the manifold separation process. 

![Dilation-Erosion Manifold Separation]({{site.baseurl}}/images/scatternet/dilation-erosion.png "Dilation-Erosion Manifold Separation")

## Conclusions

* The proposed architecture provides a method to learn object-selective and discriminative representations that allows extracting uncorrupted high frequency image representations.
* The network requires relatively very small labelled training datasets compared to deep supervised networks. We were able to get results better than current state-of-the-art ScatterNets with as low as 30 training images per class.
* The results achieved on the caltech dataset shows that our
method is robust and computationally efficient and achieves good classification accuracy
by engineering a more rich feature space.

## Future Scope
* One limitation here is that the template matching
does not scale well for larger number of classes. For further extension of this work, we plan
to engineer an architecture to overcome this limitation.