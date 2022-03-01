# A Better Sort of Yelp Photos:  
### _Using Photography 101 and Machine Learning to Help Restaurant Owners Automatically Bring the Best to the Top_  

**Problem Statement**

Given the influence of images on consumer decisions, it's surprising how many restaurants still have a slough of dark, blurry, unappetizing photos immediately visible in the gallery that opens with the "see photos" button at the top of their Yelp page.  I imagine, like me, many other Yelp users largely make decisions about what new restaurant to try based on the first images they see of the food.  Currently on Yelp, businesses who have an advertising account can sort their photo gallery, so why do so many bad and blurry photos persist near the top?  My assumption is that it takes human time plus some basic knowledge of the principles of photography to do these things.  In this project I train a model to classify food photos as good or bad using photographic first principles.  The result is expected to be a model that can classify food photos into "post-worthy" and "not so great" so that Yelp (or the restaurant owner or the app user) can automatically sort their photo galleries in a way that puts quality photos on top. 

**Methods**

*Data Selection & Pre-processing*

The primary dataset will be a set of 1000 Yelp food photos that I manually select, download, and classify into "good" and "bad" categories myself.  In order to limit variation in the model, I selected only photos of Mexican food.  Below I outline the criteria I used for my manual qualitative classification, which adheres to basic photographic principles.  While my manual classification will be somewhat subjective, these principles are well-established and I believe most people would generally agree with them (see below).   

I used an image downloading extension in my browser to classify and download the photos.  To start, I collected, 500 "good" and 500 "bad" photos to use to train and test. 

Images may need to be resized and transformed into array form for analysis in a CNN.

- Photographic Principles
    
    - Focus:  Photo should be in focus everywhere, or at least on the "subject" of the photo, such as the plate of food, or a shrimp within the dish.  Bokeh blur in the background that makes the food stand out is very good. Blurry focus over the subject or entire image is very bad.

    - Exposure:  Exposure should be even over the subject (food) without harsh shadows.  Extreme exposure (white or black) in any part of the photo is generally bad.

    - Subject:  Subject should just be the food, either centered or filling the visual frame.   Subject should not include half-eaten items, wrapped food, or any human body parts in focus.

    - Color:  Photos should either have a variety of complimentary or contrasting colors or have a simplified color set is ok if it's not primarily brown. 

    - Warth/Tint:  Generally food photos should be balanced to slightly warm (yellows and reds), as opposed to cold (blues and greens).  Exceptions include the color of the non-food background.

    - Saturation:  Color saturation should be normal to bright, but not extremely strong (no neon colors).

**Modeling**

For a modeling technique, I will try a convolutional neural net, first without a pre-trainer, then with a publicly-available Tensorflow-Keras imagenet module such as Xception.  I will explore model adjustments such as number of hidden layers, batch_size, epochs number, early stopping, dropout, and regularization to improve model performance.  

**Evaluation**

Performance will be measured using accuracy and confusion matrices.  Correctly identifying the worst photos may turn out to be preferred over a model that predicts both classes moderately well.  I will aim for an accuracy of at least 70%, with a sensitivity score above 75% (where class 1 is the "good photo" set) preferentially identify the worst photos (for filtering out or pushing to the bottom of the sort). I will post images with my classification ("good" or "bad") plus the model prediction label in the project portfolio.

**Relevance**

Why should anyone care about this project?  Restaurant review platforms and restaurant owners need to attract customers online and compelling, attractive food photographs are a large part of many customers selection process.  An automated method for sorting or filtering "good" quality photos from "bad" photos should help restaurants highlight their best food photos and attract more customers.  This information could also be used to give users feedback on the photos they upload and be used to give incentives to users who post higher quality photos. More generally, automatically identifying high-quality user-generated photos of a businesses' product amongst a sea of photos is useful to attract customers.

**Data**

- Source:  Photos publicly available on Yelp
- Format:  Initially saving data to local hard drive and saving as .jpg files.
- Data Dictionary (none yet)

**Roadmap**

- Initiail project ideas - early Feb 1
    - Originally conceived of classifying good food & bad food photos on Yelp.         
- Select or create a dataset that fits project objectives - Feb 5
     - I initially thought of using an existing dataset from Kaggle or directly through Yelp's API.  Although there was a dataset available from Yelp for research and I obtained an API key and made some initial pulls, neither method provided the dataset I needed.  I needed to manually review and label photos, which ended up being easier using an image download extension through my browser.    
- Complete data selection / labeling - Feb 12
    - Completed download and labeling 500 of each class.
- Compete Part 2 of Capstone - Feb 12
    - Completed this readme.  
- Process photos & perform EDA - iterate through Feb 20
    - Review composite histagrams of the entire data and of each class. Look over all photos just to see that they are labeled right.     
- Model runs - iterate through Feb 20
- Refine/increase/augment data - iterate through Feb 20
- Write up results & result visuals.  Feb 24
- Build streamlit Feb 28

