## Background

The COVID-19 pandemic has been one of the most deadly pandemics in the history of mankind. To date, there have been ~260 million cases worldwide resulting in ~5 million deaths and both these numbers are only expected to grow. With the emergence of new variants, even fully vaccinated individuals can contract COVID-19. This makes masks a primary resource to limit the spread of the virus. Even though mask mandates currently exist, many flout the rules and can easily get away with it. Manually checking for people wearing masks is tedious and expensive, so the development of an automated system to detect masks is of key importance. It can help save lives by establishing stricter compliance. 

### Idea

Develop a system that accurately detects the presence of a mask on multiple faces either in real-time video or static images. This approach can be used by entities ranging from restaurants to local governments to universities. For example, if you have to enter a library on campus where it is compulsory to wear masks, you will only be given permission if your scan before entering the library detects the presence of a mask. Next, while in the library, CCTV cameras can be configured to catch those that are constantly spotted without masks using facial recognition and a more sophisticated version of the model built in this project. 

### Current state-of-the-art

1. For static images

Current algorithms first perform facial recognition and then use a sophisticated R-CNN (Convolutional Neural Network) model to detect the presence of a mask once a face is successfully detected. 

2. For real-time video streams

The process is esentially the same with additional complexities. The algorithm first identifies multiple frames of the same person using facial recognition. It then uses a similar R-CNN model to detect the presence of masks in each frame. The resultant classification for each frame at any given time is computed as an average result of the previous immediate frames. Multiple frames reduce the possibility of false-classification if facial recognition fails due to multiple reasons (unclear video, face being too obscured etc.)

Current algorithms first perform facial recognition and then use a sophisticated R-CNN (Convolutional Neural Network) model to detect the presence of a mask once a face is successfully detected. 

2. For real-time video streams

The process is esentially the same with additional complexities. The algorithm first identifies multiple frames of the same person using facial recognition. It then uses a similar R-CNN model to detect the presence of masks in each frame. The resultant classification for each frame at any given time is computed as an average result of the previous immediate frames. Multiple frames reduce the possibility of false-classification if facial recognition fails due to multiple reasons (unclear video, face being too obscured etc.)

## Development Steps and Timeline of Project

- **November 30th**: Find dataset online and train model on the same
- **December 3rd**: Implement script to detect face-mask in static images
- **December 5th**: Test accuracy of model on real images (clicked by myself) and those that I found online
- **December 8th**: Implement script to detect face-mask in real-time video streams December 10th. Test accuracy of model on different videos
- **December 13th**: Try to find/ manipulate better datasets to improve the accuracy of the model and finalize presentation + project webpage

## Technical Approach & Implementation

### Preprocessing and Partioning Dataset

The dataset was found online on github. It was created by taking randomized images of faces without a mask, and then applying a mask to the face by using a custom python script (using facial landmarks to compute mask placement).
Images are then resized to 224x224 pixels each. Data is then segmented into training and test data along with appropriate labels -- mask, without_mask. 

**Example Data** 

![image](https://user-images.githubusercontent.com/47380917/146492299-ded2f308-19ab-438b-a702-f93451638965.png)

![image](https://user-images.githubusercontent.com/47380917/146492321-e953f5dd-eaf3-4259-a001-73810475651e.png)

### Building and Training Model

Tensorflow's MobileNetV2 library is used as the starting point as our base CNN. Post construction of the head of the model, layers such as AveragePooling2D, Flatten and Dense and Dropout are added in a logical manner. The head of the model is then fitted onto the base model. Using the Adam Optimizer to compile it, we then serialize the model to our disk to be used in the scripts created to detect masks in images and videos. 
The accuracy of the model is then tested on the part of our data labeled as _test_. Using multiple epochs, batch sizes and a fixed learning rate, the model is found to be ~99% accurate on our test data. 

**Model Accuracy**

![image](https://user-images.githubusercontent.com/47380917/146493010-22ed9f22-0995-4d53-bf37-82e62d5eab95.png)

### Results

**Static Images**

![image](https://user-images.githubusercontent.com/47380917/146493439-ff2fbc8a-dd2c-4faf-8076-53dcecfb773f.png)

![image](https://user-images.githubusercontent.com/47380917/146493443-212ebc70-861d-47ea-96f2-04af0fe9a664.png)

**Real-time Video Stream**

[Link To Video](https://drive.google.com/file/d/19-0osIFTxZilyt6LqVfiZTmvJ4zos2bs/view)

After analyzing our results, we can see that the model works well with multiple people in one static image - one without a mask and one without. It also works well on the side-profile image of a person found on the internet. The results on video, while accurate to some extent, can be bettered. The detector takes some time to analyze the face and change results if a person moves too quick or changes positions quicker. I assume that the multiple frame approach outlined in the current state-of-the-art section would work well in such cases. A green box on the face implies the presence of a mask while a red on implies the absence of one. The results are fairly intuitive and can be gauged from just glancing at the video-stream or static images. 

## Problems Encountered

This approach involves 2 steps. Mask detection heavily relies upon facial recognition. Due to this, there are some cases wherein the mask cannot be detected. For example, if there is low camera-quality that blurs a face or if the face is too obscured by a mask or other object and the Region of Interest (ROI) cannot be accurately located. I was also new to **keras** and **tensorflow** and had to research a fair amount on how to create an efficient model using these machine-learning libraries

## Learnings and Future Work

- Realization that mask detection in videos is more complex than it seems
- If there is a way to detect the presence of mask by bypassing the facial recognition stage, this would be an ideal approach
- Given the current scenario with COVID-19 and threat of future pandemics, the application of such a system is of key importance
- If implemented well, multiple entities can use this technology to limit the spread of COVID-19

## Project Materials

- [Presentation Slides](https://docs.google.com/presentation/d/1tHrjfLkF4Yh1GGjKZIgwefWncm7stNi3qUd1Km8lJpM/edit?usp=sharing)
- [Source Code on Github](https://github.com/yashash17/maskdetector)

## Resources

- https://github.com/prajnasb/observations/tree/master/experiements/data
- https://tryolabs.com/blog/2020/07/09/face-mask-detection-in-street-camera-video-streams-using-ai-behind-the-curtain
- https://keras.io/api/layers/reshaping_layers/flatten/
- https://keras.io/api/optimizers/
- https://www.pyimagesearch.com/2020/05/04/covid-19-face-mask-detector-with-opencv-keras-tensorflow-and-deep-learning/
- https://towardsdatascience.com/creating-a-powerful-covid-19-mask-detection-tool-with-pytorch-d961b31dcd45
