database : https://www.muratkoklu.com/datasets/ 'Durum Wheat Dataset' (bottom of the page)

# Quick Intro
This is an exploration of a Drum Wheat Database. I wanted a database containing data in a standard format as well as image to compare ML classification from text information, from images, and from videos. Data in file give a first approach to understand the classification, investigation on image will help to build keys functions, and finally findings will be used on videos to have near-real time classification


# Classification from author excel files
Classification_Features.ipynb contains data exploration, classifier choice and optimization using the excel file is present on github. 

From author metrics, a fine tuning of k-neighbours and of a random forest show a 88%+ accuracy. In all cases the remaining problem is the same, some Starchy seeds are predicted as Vitreous. Note that I ignored wavelets and Gabor image processing (Gabor = texture analysis), to focus in more usual metrics. The tendency to confounds Starchy and Vitreous seeds when Gaborlet are ignored is in fact consistent with author analysis. Indeed, he writes 'Gaborlet texture features are more prominent to identify vitreous durum wheat kernels'

# Classification from tif images

  ## Computing metrics(=stats)
Classification_Images.ipynb contains morphological and color metrics for each wheat seed identified in Vitreous, Starchy and Foreign images. However classification is very sensitive to morphological metrics, and I am not sure of their correct definitions. The formulas used for morphological metrics are taken from my understanding of the .docx file given by the author. However I am not sure if those formulas are correct as some of them highly differs from what I found on specialized website.  For the experiment, I changed on purpose de morphological metrics and it seems that their exact formulation is crucial.
Note here : I decomposed all images in subimages. A subimage correspond to one seed. This is different from usual image analysis, where one image correspond to image saved on computer (i.e a photographie of multiple seeds)

I want to contact the author to get feedback on the morphological metrics. The .ipynb is on github as communication support

 ## Using Keras 
 Keras function image_dataset_from_directory() does not work with .tif images. I have to play around, for example by converting all tif in jpeg with Pillow.

# Video
  TO DO


