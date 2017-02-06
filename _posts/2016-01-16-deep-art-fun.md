---
layout: post
title: "Deep Art fun"
date: 2016-01-16
---

Last weekend I finally took some of personal photos and artwork to *\"paint\"* them in, but not limited to, Van Gogh style. The \"painting\" part was actually an inspiring [application from **Deep learning** research](#refs). In short, the Deep learning model - a deep neural network - takes your photo (referred as ***content-image*** henceforth) and a reference style (combination of 1 or more ***style-images***) as the inputs and produces your photo in that style. I used [jcjohnson's implementation](https://github.com/jcjohnson/neural-style) of [DeepArt algorithm](#deepart) for the demo. 

## Demo
Here we have the content-image being a photo of a walking path on the top-left, the style-image is an artwork by artist Leonid Afremov on the top-right, and the walking path generated in Afremov\'s style at the bottom.
<br/>
<img src="https://raw.githubusercontent.com/hoamle/neural-style-example/master/content-imgs/exeter.jpg" height="150"> <img src="https://raw.githubusercontent.com/hoamle/neural-style-example/master/style-imgs/Afremov2.jpg" height="150">
<br/>
<img src="https://raw.githubusercontent.com/hoamle/neural-style-example/master/visually-appealing/exeter-afremov2.png" width="460">

The machine did not "paint" the picture out of the blue, it\'s an iterative learning process. In short, it starts with a blank (noisy) canvas and tries to learn prominent features in both content-image and style-image(s) and present them on the final product. That learning process is mathematically expressed as optimization process of a function representing the combined *similarity* between the output and the inputs. Optimizing such function requires an algorithm which goes through series of updating iterations, visualized in the following gif.

<img src="https://raw.githubusercontent.com/hoamle/neural-style-example/master/exeter_afremov2.gif" width="460">

## More images
{% marginnote 'mn-hardware' 'All output images are produced by NIN model + Adam optimization. If hardware constrainst is not a problem, visual results should be improved by using VGG-19 model + L-BFGS optimization.' %}

Style image: Leonid Afremov\'s
<br/>
<img src="https://raw.githubusercontent.com/hoamle/neural-style-example/master/content-imgs/pedals.jpg" height="150"> <img src="https://raw.githubusercontent.com/hoamle/neural-style-example/master/style-imgs/Afremov4.jpg" height="150">
<br/>
<img src="https://raw.githubusercontent.com/hoamle/neural-style-example/master/visually-appealing/pedals-afremov4.png" width="460">

Style image: Van Gogh\'s Starry Night 
<br/>
<img src="https://raw.githubusercontent.com/hoamle/neural-style-example/master/content-imgs/exe_quay.jpg" height="150"> <img src="https://raw.githubusercontent.com/hoamle/neural-style-example/master/style-imgs/starry_night.jpg" height="150">
<br/>
<img src="https://raw.githubusercontent.com/hoamle/neural-style-example/master/visually-appealing/exe_quay-starrynight.png" width="495">

Style image: Van Gogh\'s Starry Night
<br/> 
<img src="https://raw.githubusercontent.com/hoamle/neural-style-example/master/content-imgs/london.jpg" height="150"> <img src="https://raw.githubusercontent.com/hoamle/neural-style-example/master/style-imgs/starry_night.jpg" height="150"> 
<br/>
<img src="https://raw.githubusercontent.com/hoamle/neural-style-example/master/visually-appealing/london-starry.png" width="495">

Style image: Van Gogh\'s Wheat Field with Crows
<br/> 
<img src="https://raw.githubusercontent.com/hoamle/neural-style-example/master/content-imgs/camb.jpg" height="150"> <img src="https://raw.githubusercontent.com/hoamle/neural-style-example/master/style-imgs/vangogh_Wheat_Field_with_Crows.jpg" height="150"> 
<br/>
<img src="https://raw.githubusercontent.com/hoamle/neural-style-example/master/visually-appealing/camb-vangogh_wheatfield.png" width="575">

Style image: [creativemints](https://www.behance.net/gallery/13033419/Selected-Artworks-2013-Oil-Acrylic-Watercolor)\'s
<br/>
<img src="https://raw.githubusercontent.com/hoamle/neural-style-example/master/content-imgs/potr.jpg" height="150"> <img src="https://raw.githubusercontent.com/hoamle/neural-style-example/master/style-imgs/lostquilt_at_pinterest.jpg" height="150">
<br/>
<img src="https://raw.githubusercontent.com/hoamle/neural-style-example/master/visually-appealing/potr-lostquilt.png" width="410"> produced by NIN model @512px
<br/>
<img src="assets/img/lostquilt.png" width="410"> produced by VGG-19 model @784px

<!--Style image: Picasso\'s Self-portrait-->
<!--<br/>-->
<!--<img src="https://raw.githubusercontent.com/hoamle/neural-style-example/master/content-imgs/figure.jpg" height="300"> <img src="https://raw.githubusercontent.com/hoamle/neural-style-example/master/style-imgs/picasso_selfport1907.jpg" height="300"> => -->
<!--<img src="https://raw.githubusercontent.com/hoamle/neural-style-example/master/visually-appealing/figure-picasso_selfportr.png" height="400">-->

## Observation
* **Size matters**. The higher the output image resolution, the more details in the content-image can be explicitly expressed by the indicated style. However, memory is a *big* trade-off. Default output image size (max. 512px-wide) on an NIN took as small as 5-600MB, but a 784px image devours 3 times as much! 
* For visual appeal, (i) an **expressive** style and/or (ii) **resemblance** between content-style image pair is the key. \"Expressive\" here is not only about abstract or surreal in specific, but about texture i.e. discernible patterns in colors, strokes, blobs in general. Example work: *Leonid Afremov\'s painting, The Scream, Monet\'s water lilies,* etc. Eventually, using style-images referenced from complicated realism pieces by the old masters, like Jean Leon Gerome, usually  yields unsatisfiying output with default parameters. Secondly, although  not always, a landscape picture pairs pretty well with Starry Night or Wheat Field and the Crows; a portrait and Picasso\'s self-portrait also make a nice combination. 
* I lust over a Titan X.

## Hardware setup
On the technical bit, the main work-horse is a humble 2GB nVidia GTX 660 GPU{% sidenote 'sn-gpu' 'i.e. common video graphic card for gaming' %} on a dated LGA 775 desktop. Each image was generated in ~90 seconds (for a 512px-image) or 2-3 mins (for a 784px-image). GPU(s) with generous memory is desirable. 

It\'s *much* faster to run DeepArt algorithm on GPU(s) instead of common CPUs. Even a modern i7 K-series can take upto hour to train and generate 1 image of above sizes. However, running on CPU can take advantages of *abundant* host memory (easily >8GB on a single machine), not to mention the possibility to be accompanied with a coprocessor (eg: Xeon Phi), or running on distributed platform.

## <a name="refs">References</a>
1. <a name="deepart">[A Neural Algorithm of Artistic Style](http://arxiv.org/abs/1508.06576) (Gatys et al, 2015)</a>
2. [Artomatix](https://www.youtube.com/watch?v=VRwzE3WxA08)\'s products
2. Artist credit where it\'s due