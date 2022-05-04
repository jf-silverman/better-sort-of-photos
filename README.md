# A Better Sort of Yelp Photos:  
#### _Using Simple Photography Principles and Machine Learning to Help Restaurant Owners Automatically Bring the Best to the Top_  
_Joel Silverman_

## Problem Statement

Given the influence of photos on consumer decisions, it's surprising how many restaurants still have a slough of dark, blurry, unappetizing photos immediately visible in their main photo gallery linked at the top of their Yelp page.  It's well established that simply including images with a social media post increases engagement on social networks[[1]](#sources_cited) and since the start of COVID, the use of social media in decision making has only increased in importance[[2]](#sources_cited). Even before covid, the use of review apps to find new restaurants was second only to referals from friends and family[[3]](#sources_cited). For these reasons, Yelp app users, restaurant owners, and Yelp itself would all benefit from having an option to automatically sort restaurant photo galleries in a way that would place well-taken shots on top.  Currently on Yelp, businesses who have an advertising account can sort their photo gallery, so why do so many poorly taken photos persist?  Sorting through photos takes an owner's valuable time and selecting quality images requires some knowledge of photographic principles.  In this project I manually label a set of photos using photography principles, then train a machine learning model to classify food photos as either "post-worthy" or "not so great" so that Yelp (or the restaurant owner or the app user) can automatically sort their photo galleries in a better way.  

## Background

Despite a slough of options in the space (Google Reviews, Open Table), Yelp remains a dominant player among review plantforms.  Established in 2004, Yelp continues to grow, even surpassing its  pre-covid revenue levels in 2021 (just over $1 Billion).  Yelp boasts 100 million unique monthly users spread fairly evenly across age groups. About 45% of their customers say they consult Yelp before making purchases and over half are college-educated[[4]](#sources_cited).  The business also claims 250 million user reviews and 5.8 million claimed businesses[[5]](#sources_cited). For all these reasons, I chose Yelp for my focus although the project could well be generalized for many other use cases. 

I chose this project because it combines my interest in digital photography with my affinity for trying new restaurants.  It also was an interesting topic because I use Yelp and I thought it was something that would improve the site and app experience for users like me.  

<a id='sources_cited'></a>
**Sources Cited:** 
1. https://journals.sagepub.com/doi/pdf/10.1177/0022243719881113 
2. https://www.tandfonline.com/doi/full/10.1080/23311975.2020.1870797
3. https://www.restaurantbusinessonline.com/marketing/does-instagram-influence-where-customers-dine-out
4. https://seattleppcagency.com/marketing/is-yelp-still-relevant-in-2021/ 
5. https://www.yelp-ir.com/

## Methods

**Data Selection & Pre-processing**

Initially, I considered gathering data via Yelp's API or by utilizing a research set the company made available, but no photo quality parameters were available. Instead I downloaded 1400 photos from restaurant pages using a Chrome extension and manually labeled them as either "good" or "bad" quality photos. (see label criteria in next section). Photos were organized in specific subfolders to simplify loading for visualization and modeling.  In order to limit variation among types of food in this small dataset, I limited selection to photos from Mexican restaurants.  All images were in 1x1 ratio to avoid cropping and sizes were limited to a range of 256x256 to 348x348.  This size range supplied plenty of detail, while keeping computational work load light.

**Data cleaning**

Data cleaning was done by looking at icon views of the photos in a MacOS Finder window.  Any mislabled photos were corrected.  A few photos with text or emojis overlays were removed.  

**Label Criteria Using Basic Photographic Principles**  
While these manual labels are somewhat subjective, the underlying principles are well-established.

- **Focus:**  Photo should be in focus everywhere, or at least on the "subject" of the photo, such as the plate of food, or a shrimp within the dish.  Background could be blurred (bokeh) or not as long as the food could be seen clearly and the background was not too distracting.

- **Exposure:**  Exposure should be even over the subject (food) without harsh shadows or bright patches.  Even, diffuse light is best.

- **Subject:**  Subject should just be the food, either centered or filling the visual frame.   Subject should not include half-eaten items, wrapped food, or any human body parts in focus (arms, hands, etc.).

- **Color:**  Photos should either have a variety of complimentary or contrasting colors.  Generally a whole plate should not be one color such as brown. Generally food photos should be balanced to slightly warm (yellows and reds), as opposed to cold (blues and greens).  Exceptions include the color of the non-food background or green vegetables.  Color saturation should be normal to bright, but not extremely strong.

- **Pattern/Composition:**
A number of photographic rules make for appealing compositions (rule of thirds, rule of odds, golden ratio, etc.).  I also ruled out photos of half-eaten food or empty plates using this principle. 

## Visualization
I first loaded the photo dataset into Python using Tensorflow / Keras libraries.  I looked at random batches of labeled images to ensure they were labeled and loaded properly.  Next I made a composite mean image of all the "good" label and a composite mean image of all the "bad" label photos. I reviewed these both in color and greyscale.  The greyscale image was converted to one of Matplotlib's "perceptually uniform sequential colormaps" to more easily discern difference.  I also created histograms of the two composite images, showing the red, green, and blue pixels as separate transparencies.  After this I made a contrast image by subtracting the two composite mean images.  Lastly, I used Principle Component Analysis to examine eigen composite images and high eigen value images. All of the visualizations pointed to the importance of proper exposure and some level of framing / composition.   

## Modeling

For a modeling technique, I used a convolutional neural net, first making two models trained from scratch (model 1 and model 2), then making two models that used transfer-learning techniques (model 3 and model 4).  Model 1 just used basic CNN convolution and pooling layers.  This model achieved about 76% accuracy in the validation set after 10 epochs.  Model 2 added in model augementation and dropout to add variability and reduce model overfitting, achieving 82% accuracy in the validation set after 10 epochs.  Model 3 used transfer learning from MobileNet V2, a CNN trained on over 1.4 million images, fit to 1000 classes by Google.  The first technique, feature selection, removes the head the pre-trained model and allows final learning the new dataset.  This model (Model 3) achieved 73% accuracy after 20 epochs.  The last model was a fine-tuning transfer learning model that built on the previous model, by unfreezing more layers in the pre-trained model to exposed them to new learning from the new dataset.  This model (Model 4) achieved 83% accuracy after 20 epochs.  The percentages of accuracy and loss vary slightly each time they are run due to random effects.  

## Evaluation, Conclusions and Recommendations

Both methods of CNN (from scratch and transfer learning) achieved similar, moderate levels of performance.  These could probably be further improved through experimenting with the various parameters or layering architecture.  Part of the difficulty stems from the subjective and generalized nature of the labels, even with specific criteria.  It was interesting to note that both types of CNN performed similarly on these data.  In retrospect, it would have been better to limit photos to more similar-shaped items.  Also, it would be good to explore CNN architecture that is specific for color variation detection.  

## Notebooks
[01_Visualizations_Notebook.ipynb](code/01-Visualizations_Notebook.ipynb) This notebook shows exploratory data analysis of the image sets using example images, mean aggregate images of each class, and Principle Component Analysis "Eigen Faces" of the images.

[02_CNN_Models_From_Scratch.ipynb](code/02_CNN_Models_From_Scratch.ipynb)  This notebook covers several from-scratch CNN models, including augmentation and dropout techniques to prevent overfitting.

[03_CNN_Models_W_Transfer_Learning.ipynb](code/03_CNN_Models_W_Transfer_Learning.ipynb)  This notebook covers both feature extraction and fine-tuning techniques within a transfer learning CNN model.


## Python Libraries Used
`import os`<br>
`import pandas as pd`<br>
`import numpy as np`<br>
`import matplotlib.pyplot as plt`<br>
`import seaborn as sns`<br>
`from sklearn.decomposition import PCA`<br>
`from math import ceil`<br>
`import PIL`<br>
`from google.colab import drive`<br>
`import tensorflow as tf`<br>
`from tensorflow.keras.preprocessing import image`<br>
`from tensorflow import keras`<br>
`from tensorflow.keras import layers`<br>
`from tensorflow.keras.preprocessing import image`<br>
`from tensorflow.keras.models import Sequential`<br>
`from tensorflow.keras.callbacks import EarlyStopping`<br>

## Datasets

Folder of jpg image files downloaded from publicly available Yelp restaurant photo galleries.  Photos are all in RGB color.  Ratio are all 1:1 (square) with pixel dimensions ranging from 256x256 to 348x348.

[yelp_set3.zip](data/yelp_set3.zip)  This is a set of 1412 photos divided into training and validation sets; each subdivided into good/bad photo quality classes.

[yelp3_test.zip](data/yelp3_test.zip)  This is a set of 100 photos used for testing in some of the models.  It has not been manually classified and was never used for training or validation.

