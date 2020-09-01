Image Classification
===========
A common use of machine learning is to identify what an image represents. For example, we might want to know what type of animal appears in the following photograph.

The task of predicting what an image represents is called image classification. An image classification model is trained to recognize various classes of images. For example, a model might be trained to recognize photos representing three different types of animals: rabbits, hamsters, and dogs.

When we subsequently provide a new image as input to the model, it will output the probabilities of the image representing each of the types of animal it was trained on. An example output might be as follows:

<img src="dog.png" width="250">

|Label     |	Probability|
| :-------------: | :----------: |
|rabbit  |	0.07|
|hamster |	0.02|
|dog     |	0.91 | 


For more information [click here](https://www.tensorflow.org/lite/models/image_classification/overview#what_is_image_classification)



In this project, I used custom datasets to train and test the image classification model.
All the descriptions are given below:

   


Table of contents
==================

<!--ts-->
* [Source](#Source)
    * [Setup]()
    * [Data_collection]()
    * [Data_pre-processing]()
    * [Training]()
    * [Inference]()
        * [Single_model_inference]()
        * [Binary_model_inference]()
    * [Result]()
<!--te-->

Setup
===============
- Install Docker
- Python >= 3
- Tensorflow 2.0.0 / 2.1.0

**To use tf 2.2.0 or above, we need to edit trainign code.**


Data_collection
====================

In this project, I collected data from refrigerator of convenient store. Basically each refrigerator has 6 floors with 8 columns each. After setting up camera inside of refrigerator, I collected the images as much as possible with different angles and different position. Similalry, I tried to collect the images by changing the position os the products in each columns. 
e.g.

<img src="08181_product_w_1_1.png" width="250"> <img src="08181_product_w_2_1.png" width="250"> <img src="08181_product_w_2_6.png" width="250">


After collecting the data, I did annotations for each product because I wanted to use the same datasets for image detection project. 

<img src="11.png" width="250"> <img src="12.png" width="250">

Data_pre-processing
==========

* `Fine Crop` - Based on annotation files, I cropped the images and resized them.

<img src="fine_24.png" width="250"> <img src="fine_32.png" width="250"> 

* `Noise Crop` - I annotated the root image including noises. After that I cropped them and resized. 

<img src="noise_1.png" width="250"> <img src="noise_2.png" width="250"> 

* `Augmentation`: After cropping the images, I merged fine crop and noise crop images. After that I did [`augmentation`](). I generated around `5000` images for each classes.

<p float="left">
  <img src="/master/Image_Classification/Source/Data_pre-processing/194.png" width="100" />
  <img src="/master/Image_Classification/Source/Data_pre-processing/56.png" width="100" /> 
  <img src="/master/Image_Classification/Source/Data_pre-processing/66.png" width="100" />
</p>





**Ratio of fine and noise data should me properly managed.**

**In image `Augmentation`, hyper parameter should be modified based on dataset and test scenario.**

**I only created `5000` images for each classes because of my dataset scenario.** 







Data_pre-processing
==========



Training
===========



Inference
===========



Result
==========



| image id | class | accuracy | 
| :------------- | :----------: | -----------: |
| 1.jpg  | top_latte_pet | 0.9880806 |
| 2.jpg  | top_theblack_380_pet | 0.99987173 |
| 3.jpg  | green_smoothie_pet | 1.0 |
| 4.jpg  | letsbe_grande_latte_500_pet | 1.0 |
| 5.jpg  | Lu-10_pet | 1.0 |
| 6.jpg  | jinssanghwa_pet | 1.0  |
| 7.jpg  | georgia_original_can | 1.0 |
| 8.jpg  | hwal_pet | 1.0 |
| 9.jpg  | rice_pet | 1.0 |
| 10.jpg |  gotica_vintage_black_390_pet | 1.0 |
| 11.jpg |  vita500_pet | 1.0 |
| 12.jpg |  top_americano_pet | 1.0 |
| 13.jpg |  green_plum_pet | 0.99998486 |
| 14.jpg |  lemona_pet  1.0 |
| 15.jpg |  leblen_peach_pet | 0.9999969 |
| 16.jpg |  gotica_vintage_latte_390_pet | 1.0 |
| 17.jpg |  top_latte_can |0.9998679 |
| 18.jpg |  bacchusF_pet | 1.0 |
| 19.jpg |  bacchusF_pet |1.0 |
| 20.jpg |  condition_lady_pet |1.0 |
| 21.jpg |  cantata_americano_275_pet |0.99999976  |
| 22.jpg |  georgia_craft_latte_470_pet |0.9999933 |
| 23.jpg |  vita500_royal_pet |1.0 |
| 24.jpg |  leblen_grapefruit_pet |0.9999939 |
| 25.jpg |  miero_fiber | 1.0 |
| 26.jpg |  contrabass_latte_pet |1.0 |
| 27.jpg |  letsbe_trip_can |1.0 |
| 28.jpg |  G_original_pet |1.0 |
| 29.jpg |  G_sparkling_pet |1.0 |
| 30.jpg |  cantata_latte_390_pet |1.0 |
| 31.jpg |  smoothieking_original_pet |0.9999995 |
| 32.jpg |  condition_pet | 1.0 |
| 33.jpg |  dawn808_can | 1.0 |
| 34.jpg |  top_americano_200_can | 0.9999999 |
| 35.jpg |  starbucks_can | 1.0 |
| 36.jpg |  dawn1004_can |1.0 |
| 37.jpg |  smoothieking_pine_pet |1.0  |
| 38.jpg |  kkaesugang_can | 1.0 |
| 39.jpg |  ourtea_orange_pet |1.0 |
| 40.jpg | letsbe_mild_can | 1.0 |








