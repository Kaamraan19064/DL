# DeepFake-Detection

## Problem Statement

Deepfake techniques, which present realistic AI-generated videos of people doing and saying fictional things, have the potential to have a significant impact on how people determine the legitimacy of information presented online. These content generation and modification technologies may affect the quality of public discourse and the safeguarding of human rights—especially given that deepfakes may be used maliciously as a source of misinformation, manipulation, harassment, and persuasion. The generation of these malicious techniques will not only increase in magnitude but also ad- vance technically. Thus, we aim to device innovative strategies that will suffice the need to counter such deepfake techniques

## DATASET 

The Deepfake dataset was available on Kaggle. But the en- tire dataset was 470 GB of size. It was divided into 50 chunks of 10GB each. Using this entire data was computationally infeasible for us.So, we decided to use 4 chunks of it with total data around 40GB. After reading the metadata json for each chunk we discovered 871 real videos while rest were fake. This is because the overall data distribution had an 80:20 split ratio of fake to real. To train the models properly for generalized predictions we decided to have 50:50 fake to real ratio and we selected 871 fake videos. The total videos consisted 1742 videos in total. Now each video had 300 frames that can be read. This meant we had enough data to properly train the model

## Preprocessing 

Faces that we have extracted from frames were of different sizes so we resize each face to size 224*224*3. Like most other torch-vision models, the model we’re using (ResNeXt50)
2nd Vedant Desai
Roll Number : MT19074
Indraprastha Institute of Information Technology (IIIT-D) Delhi, India vedant19074@iiitd.ac.in
requires that input images are normalized using mean and std. deviation. So, we normalized each face using mean and std. deviation. In our classification model of sound, the features have very high dimension that we have extracted from audio due to which we were getting memory crashed error so we resized them to size 1103*40. In MFCC feature, we were getting NAN value in some pixels so we have replaced NAN value with the mean of all the pixels oh that image. And also, in Spectrogram features of audio, we were getting some minus infinity pixel so we replaced those pixels with zero value.

## Methodology

we tried was to extract the audio from video and then extract the features from those extracted audio and then passing those extracted features to our model for training. As we are giving features of sound to our models, which are nothing but images and we know that CNN works better than other models like RNN, LSTM, etc. for image classification because CNN extracts spatial information whereas, RNN extracts temporal features and also in the deep network of RNN there is also a problem of vanishing gradient whereas in CNN starting convolution layers gives us finer information and deep convolution layers gives us coarser information about the image. By combining coarser and finer information, we can
classify the image more appropriately.
So we decided to use a simple CNN-based model for classification, simple because we have 1220 videos, which means only 1220 images of audio features for training. We applied three different features of sound to our training model. To build a baseline for our audio classification, we simply passed the raw data i.e., the simple waveform of audio as an image to our model, and we got the validation accuracy as 57.43%. In the second model, we passed the MFCC features of audio as an image to our model, and we got the validation accuracy as 77.83%. In the third model, we passed the Spectrogram features of audio as an image to our model, and we got validation accuracy as 83.04%.

## Result 

We can see the result in docs folder.

https://github.com/Kaamraan19064/DeepFake-Detection/tree/master/Docs
