---
layout: post
title: Discriminatory Scatternet Framework For Object Classification
---

<link rel="stylesheet" type="text/css" href="{{ site.baseurl }}/post.css" />

Object classification is the task of classifying images by extracting features from image data.
An image classification system must have the capacity to distinguish between similar looking
image regions while being invariant in its response to the appearance-altering transformation.
The fundamental challenge for any such system lies within this simultaneous requirement for
both invariance and specificity.

Deep learning networks ignore the geometric considerations and
compute descriptors having suitable invariance and stability to geometric transformations
using (end-to-end) learned multi-layered network filters. These deep learning networks in
recent years have come to dominate the previously separate fields of research in machine
learning, computer vision, natural language understanding and speech recognition.
Despite the success of the deep networks, there remains a fundamental lack of
understanding in the design and optimization of these networks which makes it difficult
to develop them. Also, training of these networks requires large labeled datasets which in
numerous applications may not be available.

In this Framework, we propose a hybrid semi-supervised architecture comprising of
a manifold separation technique and ScatterNet for Image Classification. The network
first learns the deformable template for foreground object of interest using active basis
model [13] which undergoes morphological operations and is used to learn translation
invariant representations that include separability between the object of interest and
background clutter within an image. The proposed network is shown to outperform Mallat’s
ScatterNet [7] and DTCWT ScatterNet [12] on caltech-101 image dataset.

