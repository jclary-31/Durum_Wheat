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

I contacted the author to get feedback on the morphological metrics. The .ipynb is on github as communication support. However I never get anys answers.  Conclusion here is that computed metrics does not work. However some of the metrics computed by the authors, make no sense. For example, they measures negative ellispe's eccentricity, which is by definition impossible.

If computing metrics is an dead end, there is still another ways to exploit tif images, i.e. using keras framework (next part)

 ## Using Keras 
 Keras function image_dataset_from_directory() does not work with .tif images. There is two ways to bypass this issues. First one is to convert all tif in jpeg with Pillow, and save them in another directory, but this require some space on the computer. The second way is to create a dataframe containing .tif adress and then exploit datagen.flow_from_dataframe() function.

One could then develop is own deep learning algorithm, which would require a lot of time, and probably more data. Another ways, is to exploit already existing deep learning models, and especially the ones specialized in image processing. Test with VGG16 pretrained model is excellent as I reached a 98% precision. I also want to test another well know model, Resnet50, just for comparison.

<p align="center">
 <img width="800" src=Keras_output_exple.png>
 </p>

# Video
  TO DO
  Here I will use the Keras framework and the fine tuned model in the previous section. The main job is to make a code to read videos  and the apply the fined model for autmatic dectection. One open question (for now) is how deal with consecutive images (image i and image i+1) which shared a large amount of data. Should I process the two image separately and check for difference or should I process only the part of image i+1 that does not exist in image i ? 

