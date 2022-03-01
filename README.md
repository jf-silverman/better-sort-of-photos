# A Better Sort of Yelp Photos:  
#### _Using Photography 101 and Machine Learning to Help Restaurant Owners Automatically Bring the Best to the Top_  
_Joel Silverman_

## Problem Statement

Given the influence of images on consumer decisions, it's surprising how many restaurants still have a slough of dark, blurry, unappetizing photos immediately visible in their main photo gallery linked at the top of their Yelp page.  While Yelp app users deserve to be able to see all the photos posted to a business, app users, business owners, and Yelp itself would all benefit by introducing an automated way to sort restaurant food photo galleries in a way that would place well taken shots on top.  Currently on Yelp, businesses who have an advertising account can sort their photo gallery, so why do so many bad and blurry photos persist near the top?  It takes an owner's valuable time plus knowledge of photographic principles to do these things.  In this project I manually label a set of photos using photography principles, then train a machine learning model to classify food photos as either "post-worthy" and "not so great" so that Yelp (or the restaurant owner or the app user) can automatically sort their photo galleries in a better way. 

## Background
- Discuss Yelp as a business, it's revenue, it's market 
- Discuss survey of how people choose new restaurants
- Discuss how important photos are to reviews
- Discuss how important social media to consumer purchase since covid
 founded in 2004
- up to 73 million new monthly users on the mobile app (100 M unique monthly users
- 45% of their customers say they consult Yelp before buying (compared with 63% for Google
- demographics are evenly distributed.  https://seattleppcagency.com/marketing/is-yelp-still-relevant-in-2021/ 
$1.03 B Revenue in 2021 (above Pre-Pandemic levels) https://www.macrotrends.net/stocks/charts/YELP/yelp/revenue  
2018 Small independent study by YouGov found 30% surveyed how guests found new restaurants (2nd most common after fam & friends
2020 image content increases engagement on social networks:
https://journals.sagepub.com/doi/pdf/10.1177/0022243719881113 
2021 social media in decision making gains importance after start of covid-19
https://www.tandfonline.com/doi/full/10.1080/23311975.2020.1870797 

Sources Cited: 


## Methods

**Data Selection & Pre-processing**

The primary dataset will be a set of 1000 Yelp food photos that I manually select, download, and classify into "good" and "bad" categories myself.  In order to limit variation in the model, I selected only photos of Mexican food.  Below I outline the criteria I used for my manual qualitative classification, which adheres to basic photographic principles.  While my manual classification will be somewhat subjective, these principles are well-established and I believe most people would generally agree with them (see below).   

I used an image downloading extension in my browser to classify and download the photos.  To start, I collected, 500 "good" and 500 "bad" photos to use to train and test. 

Images may need to be resized and transformed into array form for analysis in a CNN.

**Photographic Principles**
    
- Focus:  Photo should be in focus everywhere, or at least on the "subject" of the photo, such as the plate of food, or a shrimp within the dish.  Bokeh blur in the background that makes the food stand out is very good. Blurry focus over the subject or entire image is very bad.

- Exposure:  Exposure should be even over the subject (food) without harsh shadows.  Extreme exposure (white or black) in any part of the photo is generally bad.

- Subject:  Subject should just be the food, either centered or filling the visual frame.   Subject should not include half-eaten items, wrapped food, or any human body parts in focus.

- Color:  Photos should either have a variety of complimentary or contrasting colors or have a simplified color set is ok if it's not primarily brown. 

- Warth/Tint:  Generally food photos should be balanced to slightly warm (yellows and reds), as opposed to cold (blues and greens).  Exceptions include the color of the non-food background.

 - Saturation:  Color saturation should be normal to bright, but not extremely strong (no neon colors).

## Modeling

For a modeling technique, I will try a convolutional neural net, first without a pre-trainer, then with a publicly-available Tensorflow-Keras imagenet module such as Xception.  I will explore model adjustments such as number of hidden layers, batch_size, epochs number, early stopping, dropout, and regularization to improve model performance.  

## Evaluation

Performance will be measured using accuracy and confusion matrices.  Correctly identifying the worst photos may turn out to be preferred over a model that predicts both classes moderately well.  I will aim for an accuracy of at least 70%, with a sensitivity score above 75% (where class 1 is the "good photo" set) preferentially identify the worst photos (for filtering out or pushing to the bottom of the sort). I will post images with my classification ("good" or "bad") plus the model prediction label in the project portfolio.

## Relevance

Why should anyone care about this project?  Restaurant review platforms and restaurant owners need to attract customers online and compelling, attractive food photographs are a large part of many customers selection process.  An automated method for sorting or filtering "good" quality photos from "bad" photos should help restaurants highlight their best food photos and attract more customers.  This information could also be used to give users feedback on the photos they upload and be used to give incentives to users who post higher quality photos. More generally, automatically identifying high-quality user-generated photos of a businesses' product amongst a sea of photos is useful to attract customers.

## Conclusions and Recommendations


## Notebooks
[api_functions.ipynb](/code/xyz): Notebook




**Data**


- Format:  Initially saving data to local hard drive and saving as .jpg files.
- Data Dictionary (none yet)


## Datasets
- Source:  Photos publicly available on Yelp
- Storage: github

[yelp_set3.zip]('data/yelp_set3.zip'): Folder of jpg image files downloaded from publicly available Yelp photo galleries.


|FEATURE|TYPE|DESCRIPTION|
|---|---|---|
|**datetime**|*object*|Date an
