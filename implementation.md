---
layout: default
title: Implementation
---
# Main Technologies #
As shown in our research, we decided to use `Android Studio` as our IDE with Java as its language.

<img src="/2023/group43/assets/images/implementation/Android_Studio.png" width="200" height="200">

# Dependencies and Tools #

# Features #
## Router Detection ##
This is the main feature of our application. By scanning over the routers, it detects the physical components of them, and gives appropriate labels. On the labels, it states the name of the component, and the accuracy of the detection. This feature can be segmented into 2 distinct units: 
- **Object Dector Processor**: Using the camera to *scan object, create overlays on the detected components, and label them accordingly*. The code for this feature is present in the `com.example.arapprouterjava/junior/java/objectdetector` package, with `ObjectDetectorProcessor.java` as the main file, and `ObjectGraphic.java` as its dependency. The two classes in this package are responsible for processing and giving labels to the detected objects. However, without an actual ML model to work with, this feature is incomplete. For instance, it can create overlays on the detected objects, but it cannot label them.
- The second unit is the **ML model** itself. This model is responsible for recognizing the physical components of the router. In our project, this model is trained separately following the Transfer Learning method, using the MobileNetV2 model, and is the imported into our project in the `app/assets/custom_models/MobileNetV2_transfer_learning.tflite`.

The main code for connecting these 2 units is present in the 'LivePreviewActivity.java' file. from line 346-356. This code basically loads the recognition model for the detector, so that camera can correctly detected and label the router.

## Barcode Scanning ##
This is a secondary feature of our application. It allows the junior engineer to *scan the barcode behind the router, which fetches the router's serial number*. This serial number is then used to fetch the router's details from the database. The code for this feature is present in the `com.example.arapprouterjava/junior/java/barcodescanner` package, with `BarcodeScannerProcessor.java` as the main file, and `BarcodeScanningGraphic.java` as its dependency. The two classes in this package follow a similar structure to the Object Detector feauture, with the `BarcodeScannerProcessor.java` being responsible for processing the barcode, and the `BarcodeScanningGraphic.java` for creating overlays on the detected barcode.

## User Manual ##
This is a complementary feature of our application. *It provides a wide selection of user manual for the junior engineer to select from and displays them as a readable pdf, which guides him/her on how to solve router issues*. The code for this feature is present in `com.example.arapprouterjava/junior/java/preference/ManualPage.java`, this code is mainly responsible of displaying the pdf file, given its path. The pdf files are stored in the `app/assets/user_manuals` folder, and we fetch them using the `AssetManager` class.

## Call for Help ##
This is a complementary feature of our application. It allows the junior engineer to *call for help in case he/she is unable to solve the router issue*. There are some conditions necessary for this feature to work:
- The junior engineer must have some type of connectivity/way to access internet to make a video call
- There must be an open meeting present in Jitsi, which the junior engineer can join

The code for this feature is present in the `com.example.arapprouterjava/junior/java/LivePreviewActivity.java` file on line 235-262. This code is responsible for joining into any open meeting in Jitsi, otherwise it return a message saying "No meetings available, please try again later". More information about how the *call procedure* works can seen in [Video Conferencing](#video-conferencing).

## Video Conferencing ##


# Implementation Showcase 
{% include view-slideshow.html %}

# Technical Video Demo # 

