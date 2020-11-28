---
layout: post
title:  "Edge Detection In OpenCV"
categories: [ Computer Vision  ]
categories: [ Robotics]
tags: [blog_post]
---

Conventional image processing involves extracting all features in a still image, otherwise observable qualitatively by naked eyes, using computationally implemented mathematical algorithms.

The most common image features include:

* **Blobs** - regions with distinctive and colors/pattern of 
* **Edges** - boundary between different regions of an image with sharp change in pixel values
* **Corners** - inflection-points for sharp gradients in image gradients 

### Edges in an Image

**Edges** in an image are the most distinctly observable among all features and the mathematics is intuitive as well. A sudden change or discontinuity in the image intensity is defined as an edge, usually a border between two different objects in the scene or different depth projections of the same. 

The edges in an image are due to sudden change in image intensity due to **a)** change in depth **b)** object boundaries **c)** surface projection. While ideally a step change in the intensity is expected, higher resolution images may have more blurred edges causing more difficulties in detecting the same. Common reasons for blurred and indistinct edges include penumbrial blur, 




