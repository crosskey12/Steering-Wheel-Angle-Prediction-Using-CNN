# Steering-Wheel-Angle-Prediction-Using-CNN
In this project we have discussed a new approach towards the problem using Convolutional LSTM.
We have also compared existing models like VGG19, ResNet50 using transfer learning. A CNN
architecture was also developed by NVIDIA in this subject, often regarded as PilotNet, has also been
compared. Our model has been partially inspired by this model but has proven to give better results on
Udacity self-driving car simulator dataset.
However, this model is far from perfect and there is substantial research that still needs to be done on the
subject before models like these can be deployed widely to transport the public.

## Dataset
The data is recorded using Udacity’s self-driving car simulator. It is recorded on lake
track by driving 3-5 laps. The Udacity self-driving car is fitted with 3 front cameras which
would take the images. The images would be saved on the SSD. The model would extract the
steering angles via the vehicle’s controller area network (CAN) bus at different time stamp,
where it’s value ranges from -1 to +1. This will be stored in a csv file along with other
attributes. The attributes in our data are (center, left, right, steering angle, throttle, reverse,
speed) where center, left and right columns consist of network path of images.

## Data Preprocessing
ince we drive straight most of the time the steering angle is accordingly distributed.
We need to have a fair distribution in order to eliminate the bias to drive straight all the time.
Hence, we have modified the data such that there are significant amount of left steering angle
and right steering angle. The below histogram shows us the steering angles before and after
modifying the dataset. We have also resized the data to (200,66,3) and normalize it before
converting our 3D data to 5D after augmentation in order to give appropriate input to the
layer.

## Data Augmentation
The amount of data required to train a self-driving car model for every track is
simply too great to handle in practice. Additionally, it is not feasible to collect data for all
weather and road conditions. Therefore, a concept for generalizing the behavior across several
tracks must be developed. To introduce randomness and variation into our dataset we have
augmented images based on 0.5 probability for each type of augmentation
Zoom - In the training set, about 30% of the image's top third is trimmed and passed.
Brightness - The brightness enhancement can be quite beneficial when applied generally to
weather circumstances with bright sunny days or gloomy, lowlight conditions. Below is a
screenshot showing the code excerpt and brightness increase. In a similar vein, I reduced the
brightness for various circumstances.
Flip - The image is horizontally inverted (i.e., the dataset receives the mirror image of the
original image). This serves to teach the model for turns of a similar nature on opposite sides
as well.
Shift – The image is shifted horizontally and vertically by 10%.

## Results 

Loss Function - Mean Squared Error
Optimizer - Adam
Models – We have trained and tested pretrained vgg16 (Imagenet weights), pretrained resnet50 (Imagenet
weights), pilotnet (NVIDIA model) and our own model named larva. We optained best accuracy by larva
(mse= 0.0198) , while pilotnet stood to be next in line (mse(best) = 0.0281). Resnet50 (mse=0.0450) and
VGG16 (0.0742) were not even close to both models.
