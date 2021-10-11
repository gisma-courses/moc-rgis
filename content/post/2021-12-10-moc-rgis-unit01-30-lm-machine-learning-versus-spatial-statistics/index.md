---
title: 'LM | Machine Learning versus spatial statistics'
author: Chris Reudenbach
date: '2021-10-10'
slug: []
categories:
  - courses
  - unit01
tags:
  - rgis
  - unit01
toc: true
subtitle: 'thats a subtitle'
description: 'description and what a description'
image: '/assets/images/01-splash.jpg'
---
<style>.myDiv {margin-top: -35px;margin-right: -40%; text-align: right;}</style>
<div class="myDiv">
*Source: [Dr. John Snow](https://en.wikipedia.org/wiki/John_Snow) [via wikimedia](https://w.wiki/QtV)*
</div>

Now that we have learned the basic concepts of distance, neighborhood and filling spatial gaps, let's take a look at interpolating or predicting values in space.

For many decades, deterministic interpolation techniques (inverse distance weighting, nearest neighbor, kriging) have been the most popular spatial interpolation techniques. External drift kriging and regression kriging, in particular, are fundamental techniques that use spatial autocorrelation and covariate information, i.e. sophisticated regression statistics.

Machine learning algorithms like random forest have become very popular for spatial environmental prediction. The reason is that they are able to take into account non-linear and complex relationships, and thus compensate for certain disadvantages that are present in the usual regression methods.



## Proximity Concepts

### Voronoi polygons -- dividing space geometrically
[Voronoi polygons](https://en.wikipedia.org/wiki/Voronoi_diagram){:target="_blank"} (aka Thiessen polygons) are an elementary method for geometrically determining *proximity* or *neighborhoods*. Voronoi polygons (see figure below) divide an area into regions that are closest to a given point that belongs to a set of irregularly distributed points. In two dimensions, a Voronoi polygon encompasses an area around a point, such that every spatial point in the polygon is closer to this point than to any other point in the set. Such constructs can also be formed in higher dimensions, giving rise to Voronoi polyhedra.

 ![](images/suisse1.html){width=100% height=100%}

  <figcaption>The blue dots are a typical example of irregularly distributed points in space -- in this case, rain gauges in Switzerland. The overlaid polygons are the corresponding Voronoi segments that define the corresponding closest geometrical areas (gisma 2021)" </figcaption>
</figure>

Since Voronoi polygons correspond to an organizational principle frequently observed in nature (e.g. plant cells) and in the spatial sciences (e.g. [central places](https://en.wikipedia.org/wiki/Central_place_theory){:target="_blank"}, according to Christaller), there are manifold possible applications. Two things must be assumed, however: First, that nothing else is known about the space between the sampled locations and, second, that the boundary line between two samples marks the point of equal distance.

Voronoi polygons can also be used to delineate catchment areas of shops, service facilities or wells, like in the example of the Soho cholera outbreak. Please note that within a polygon, one of the spatial features is isomorphic, i.e. the spatial features are identical. 

But what if we know more about the spatial relationships of the features? Let's have a look at some crucial concepts.

### Spatial interpolation of data
*Spatially interpolating* data points provides us with a modeled quasi-continuous estimation of features under the corresponding assumptions. But what is spatial interpolation? This means using values that are known to calculate unknown neighboring values. Most of these techniques are among the most complex methods of spatial analysis, so we will deliberately limit ourselves here to a basic overview of the methods. Some of the best-known and common interpolation methods found in spatial sciences are *nearest neighbor* *inverse distance*, *spline interpolations*, *kriging*, and *regression methods*.

### Continously filling the gaps by interpolation
To get started, take a look at the following figure, which shows you (in addition to the overlaid Voronoi tessellation) six different interpolation methods to derive the spatial distribution of precipitation in Switzerland. 

![](images/suisse6.html){width=900px height=1280px}
<figure>
  <figcaption>The blue dots are a typical example of irregularly distributed points in space -- in this case, rain gauges in Switzerland. The size of each dot corresponds to the amount of precipitation in mm. The overlaid polygons are the corresponding Voronoi segments that define the corresponding closest geometrical areas (gisma 2021)" 
top left: Nearest neighbor interpolation based on 3-5 nearest neighbors, top right: Inverse Distance weighting (IDW) interpolation method
middle left: AutoKriging with no additional parameters, middle right: Thin plate spline regression interpolation method
bottom left: Triangular irregular net (TIN) surface interpolation, bottom right: additive model (GAM) interpolation 
  </figcaption>
</figure>


In the example of precipitation in Switzerland, the positions of the meteorological measuring stations are fixed and cannot be freely chosen.

When choosing an appropriate interpolation method, you need to pay attention to the following properties of the samples (distribution and properties of the measuring points):

* **Representativeness of measuring points:** The sample should represent the phenomenon being analyzed in all of its manifestations.
* **Homogeneity of measuring points:** The spatial interdependence of the data is a very important basic requirement for further meaningful analysis. 
* **Spatial distribution of measuring points:** The spatial distribution is of great importance. It can be completely random, regular or clustered. 
* **Number of measuring points:** The number of measurement points depends on the phenomenon and the area. In most cases, the choice of sample size is subject to practical limitations.

What makes things even more complex is that representativeness, homogeneity, spatial distribution and size are all interrelated. For example, a sample size of 5 measuring stations for estimating precipitation for all of Switzerland is hardly meaningful and therefore not representative. Equally unrepresentative would be selecting every measuring station in German-speaking Switzerland to estimate  precipitation for the entire country. In this case, the number alone might be sufficient, but the spatial distribution would not be. If you now select every station at an altitude below 750 m asl, the sample could be correct in terms of both size and spatial distribution, but the phenomenon is not homogeneously represented in the sample. An estimate based on this sample would be clearly distorted, especially in areas above 750 m asl. In practice, virtually every natural spatially-continuous phenomenon is governed by stochastic fluctuations, so it can only be described mathematically in approximate terms.


### Machine learning
Machine learning methods such as random forest can also produce spatial and temporal predictions (i.e. produce maps from point observations). 
These methods are particularly robust because they take spatial autocorrelation into account, which can improve predictions or interpolations by adding geographic distances. This ultimately leads to better maps with much more complex relationships and dependencies.
In the simplest case, the results are comparable to the well-known model-based geostatistics. The advantage of ML methods over model-based geostatistics, however, is that they make fewer assumptions, can take non-linearities into account and are easier to automate.
![](images/ML_interpol.png){width=100% height=100%}
<figure>
  <figcaption> The original dataset (top left) is a terrain model reduced to 8 meters with 48384 single pixels. 
For interpolation, 1448 points were randomly drawn and interpolated with conventional kriging (top right), support vector machines (SVM) (middle left), neural networks (middle right), and two variants of random forest (bottom row). In each method, only the distance of the drawn points is used as a dependency.   
  </figcaption>
</figure>

Every interpolation was applied using the "default" settings. Tuning could possibly lead to significant changes in all of them.
The error measures are correlated to the visual results: Kriging and the neural network show the best performance, followed by the random forest models and the support-vector machine.

<table>
 <thead>
  <tr>
   <th style="text-align:left;"> model </th>
   <th style="text-align:left;"> total_error </th>
   <th style="text-align:left;"> mean_error </th>
   <th style="text-align:left;"> sd_error </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> Kriging </td>
   <td style="text-align:left;"> 15797773.0 </td>
   <td style="text-align:left;"> 54.2 </td>
   <td style="text-align:left;"> 67.9 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Neural Network </td>
   <td style="text-align:left;"> 19772241.0 </td>
   <td style="text-align:left;"> 67.8 </td>
   <td style="text-align:left;"> 80.5 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Random Forest </td>
   <td style="text-align:left;"> 20540628.1 </td>
   <td style="text-align:left;"> 70.4 </td>
   <td style="text-align:left;"> 82.5 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Normalized Random Forest </td>
   <td style="text-align:left;"> 20597969.8 </td>
   <td style="text-align:left;"> 70.6 </td>
   <td style="text-align:left;"> 82.7 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Support Vector Machine </td>
   <td style="text-align:left;"> 21152987.7 </td>
   <td style="text-align:left;"> 72.5 </td>
   <td style="text-align:left;"> 68.3 </td>
  </tr>
</tbody>
</table>

## Video
Placeholder, for now:

{{< moc-rgis "/moc-rgis/assets/pdfs/GeoAI-01-01_Intro.pdf" >}}


## Unit 1 slides

{{< moc-rgis "/moc-rgis/assets/pdfs/GeoAI-01-01_Intro.pdf" >}}


## Additional references
Get the Most Out of AI, Machine Learning, and Deep Learning [Part 1](https://www.youtube.com/watch?v=KiKjforteXs){:target="_blank"} (10:52) and [Part 2](https://www.youtube.com/watch?v=Ys33AhNDwC4){:target="_blank"} (13:18)

[Why You Should NOT Learn Machine Learning!](https://youtu.be/reY50t2hbuM){:target="_blank"} (6:17)

[GeoAI: Machine Learning meets ArcGIS](https://youtu.be/aKq50YM8a8w){:target="_blank"} (8:50)