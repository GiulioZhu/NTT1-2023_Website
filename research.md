---
layout: default
title: Research
---
# Related Project Review
Due to the nature of the project, we  decided to conduct a review of the technologies and tools that related to our field. This allowed us to understand the capabilities of the tools and how they can be used to achieve the project goals. Among all of the open source tools, we found [Google AR Core](https://github.com/google-ar/) and [ML Kit](https://github.com/googlesamples/mlkit) to be the most relevant ones. 

## Google AR Core
When we were given the requirements, this was the first tool that came to our minds. **AR Core** is a platform that allows developers to build *augmented reality experiences*. It is available for Android and iOS devices. Among its open source projects, we found [Augmented Images](https://github.com/google-ar/arcore-android-sdk/tree/master/samples/augmented_image_java) and [Camera Sharing](https://github.com/google-ar/arcore-android-sdk/tree/master/samples/shared_camera_java) projects to be the most relevant ones to our case[^1].

**Augmented Images** is a project that allows users to *detect and track images in the real world*. This is a very useful feature for our project as we need to detect and track the labels on the routers. This allows junior engineers to scan for router labels and gather essential information about the routers.

On the other hand, **Camera Sharing** is a project that allows users *to share the camera feed between two devices*. This is a **key feature** for our project as we need a method to establish communication between the junior engineer and the senior engineer. It allows the senior engineer to see what the junior engineer is seeing and guide them through the process.


In the development process with AR Core we found out that AR Core, despite its wonderful features, it *deviated from our vision of the software*. Our app needed **object detections** and **supporting graphic overlays** to display information, which AR Core didn't provide. We also found out compatibility issues with AR Core, which made it difficult to implement the features we wanted. This led us to transition into a more practical tool, ML Kit.

## ML Kit
**ML Kit** is a platform that allows developers to build *machine learning models* and *integrate them into their applications*. It is available for Android and iOS devices. Among its open source projects, we found out that [ML Kit Vision App](https://github.com/googlesamples/mlkit/tree/master/android/vision-quickstart) matches most of our requirements. Some of its most relevant features are: **object detection** and **barcode scanning**[^2]. 

**Object Detection** is a feature that allows users to *detect and track objects in the live camera feed*. The detection model is based on a trained ML model, which means that we can train the model to recognize specific features of the routers.

**Barcode Scanning** is a feature that allows users to scan and process barcodes. This is also an important feature in our project, because it's *scalable*. All routers have barcodes, so it's universally applicable. 

It's worth noting that ML Kit is a **more general** tool than AR Core, so it can be used in a wider range of applications. *It's edge over AR Core is that it incorporates multiple features in a single compact app, which best suited our needs*. 
‌

# Technology Review
In the development process, we explored a variety of technologies and ways that could be used to achieve the project goals. 

We considered our project *persona* and *scenario* and we discovered that **mobile development** was the solution. Among it's advantages, we found that it's **scalable**, **portable** and **cost-effective**. Because junior engineers are always on the move, it's important that they *have access to the app at all times*, also it's important that the app is *easy to use* and *doesn't require any additional hardware*. For these reasons, we excluded **tablets** and **ar goggles** from our list of potential solutions.

## Devices
Our client gave us the freedom to choose Android or IOS as the operating system for our application. Since we were aiming moderately complicated application, we aimed to build a native phone application as it would be more performant and allow us to easily leverage native APIs to access device features[^5]. Therefore, we planned to employ either *Java* or *Swift* when developing our application instead of cross platform UI libraries such as *React native* or *Flutter*.

Both the Android SDK and IOS SDK provided all the necessary tooling and APIs that we needed to fulfil the client requirements. For instance, one of our main objectives was to use a custom machine learning model to detect router features and attach labels to objects for which Android’s *ML kit* and IOS’s *Core ML* would suffice. Furthermore Android and IOS both had excellent documentation, third party library support and large and active developer communities that ensured that we could efficiently and quickly implement features and resolve bugs.

Our final decision came down to the devices readily available to us for development and the choice of programming language used with each operating system’s SDK.

Two out of three teammates were using Android devices which would allow them to quickly download the app to their devices and test its functionality - something we needed to do quite often with an App that scanned the environment using the camera and viewfinder. Furthermore, for native IOS development a relatively modern apple(Mac OS) computer is required to install the *Xcode IDE* to develop applications[^6]. Since our team had 2 Windows machines and 1 Macbook, we decided it would be wise to develop an Android application since all our devices were capable of running Android Studio and thus we could independently develop features of our app. Android studio also has built in support for emulators which can be used to see how code changes reflect in our application in real time.

Android development is done primarily in Java/Kotlin[^7] while IOS development is done in Apple’s Swift programming language[^8]. As our team had previous experience working with Java due to our university module, we decided to opt for Android development as it would involve less of a learning curve than learning a completely new programming language such as Swift (and its associated Swift UI framework). This ensured we could quickly dive into the development process and start implementing features. Due to Google’s deep involvement with the Android project, we also received the benefit of deep integration within Google’s ecosystem of technologies such as *Firebase*[^9] and *Tensorflow*[^10]. This made it relatively straight forward for us to implement these technologies in our application.

## Algorithms
A core feature of our application was to recognise Router features and apply labels over them. To achieve this, a custom machine learning model capable of recognising these features was needed. *ML kit*, the machine learning framework native to our Android application, required a *Tensorflow lite model* for object detection which we had to create using the Tensorflow machine learning framework[^11]. 

To train a machine learning model We initially planned to use Firebase ML SDK. Although this service would have simplified the training process, it is primarily geared towards cloud hosted models and Google recommends using ML kit SDK for our target features of Object detection and Barcode scanning[^12]. 

For the machine learning model architecture we opted for *MobileNetV2* which is convolutional neural network tuned to work on resource constrained devices such as mobile and IOT [^13]. Its streamlined architecture enables swift inference, crucial for real-time object detection applications on phones. Despite its compact size, MobileNetV2 maintains competitive accuracy, ensuring reliable performance without burdening the device's hardware. This is particularly beneficial for mobile applications where responsiveness and battery life are paramount. We also considered architectures such as MobileDET, Yolo and SSD (Single Shot Multibox Detector) however despite the speed and accuracy advantages over MobileNet, their relative complexities and higher resource requirements made them less suited for our use case. 

We had the option of training the MobileNetV2 model from scratch but that would entail a long training period due to the computing resources at our disposal. There was also the risk of creating a less accurate model due to our limited training data. We therefore opted for a transfer learning approach of creating our custom model[^14]. For this we downloaded a headless version of the MobileNetV2 model with the final classification layer removed, which we fine tuned on our dataset of router features. This approach ensured that our model could take advantage of the existing model’s learned feature and removing the need to start from scratch by training an entirely new model[^15]. By only training the newly-added classifier layers and freezing layers of the base model, transfer learning provided us a way to quickly create an accurate model in an efficient manner. 

For our AI guidance feature we converted a user selected image into base64 and then sent the query to the *GPT 4 vision API*. The API response would then be displayed to the user in the text view. We set the model *temperature* to zero and made use of prompt engineering techniques to prevent the large language model from hallucinating or demonstrating unpredictable behaviour[^16].


## Programming Languages

## Frameworks
Among our list of possible frameworks, we considered **Unity**, **Vuforia**, and **Android Studio** as potential solutions. 

**Unity** is a cross-platform engine that allows developers to build *3D and 2D games, apps, and experiences for entertainment, film, automotive, architecture, and more*. It uses C# and C++, and it supports a variety of platforms, including android and ios[^3]. It provides a robust and intuitive development environment, which is beginner-friendly and efficient for experienced developers. It also boasts of an extensive asset store contributed by the Unity community offering a wide range of completed assets to work with which simplifies the development process. It also allows performance optimization with its built-in tools, which ensures smooth performance across devices[^4].

**Vuforia** is a scalble AR content creation solution that transforms existing 3D CAD or product for mobile devices that enables the creation of augmented reality applications. Some of its features include *image targets, cloud recognition service, and barcode scanners*. This allows developers to quickly create recognition models, since cloud recognition service allows developers to upload images to the cloud and get recognition results in real-time without any requirement on training. It also supports a wide range of devices and platforms, including Android, iOS, and UWP and also provides a wide range of APIs and SDKs for developers to work with, which makes it a versatile tool for AR development.

**Android Studio** is the official IDE for Android app development, based on IntelliJ IDEA. It provides a comprehensive development environment for Android app development, with features like *code completion, refactoring, and lint tools*. It also provides a visual layout editor, which allows developers to create layouts by dragging and dropping UI elements. It also provides a wide range of tools for debugging and testing, which makes it a powerful tool for Android app development.

## Libraries

## APIs


<!-- i will add a comparison table here - Giuli, link: https://www.w3schools.com/howto/howto_css_comparison_table.asp -->


# References
[^1]: “AR Core,” Google Developers. https://developers.google.com/ar
[^2]: “ML Kit,” Google Developers. https://developers.google.com/ml-kit
[^3]: Unity Technologies, “Unity - Unity,” Unity, 2019. https://unity.com
[^4]: X. Web, “Top Advantages of Using Unity for Game Development,” Medium, Jun. 19, 2023. https://medium.com/@xceltecweb/top-advantages-of-using-unity-for-game-development-bd64b6a3004
[^5]:P. Manager, “Native App vs Cross-Platform: How to Make a Choice,” JatApp, Feb. 20, 2019. https://jatapp.co/blog/native-or-cross-platform-app-development/ (accessed Apr. 07, 2024).[^6]:Apple, “Xcode - Support - Apple Developer,” Apple.com, 2020. https://developer.apple.com/support/xcode/
[^7]:Apple, “Swift,” Apple. https://www.apple.com/lae/swift(accessed Apr. 07, 2024).
[^8]:Google, “Kotlin and Android,” Android Developers. https://developer.android.com/kotlin
[^9]:Google, “Add Firebase to your Android project  |  Firebase,” Firebase, 2019. https://firebase.google.com/docs/android/setup
[^10]:Google, “Custom Models with ML Kit,” Google Developers. https://developers.google.com/ml-kit/custom-models
[^11]:Google, “TensorFlow Lite guide,” TensorFlow. https://www.tensorflow.org/lite/guide
[^12]:Google, “Migration guide | ML Kit,” Google for Developers. https://developers.google.com/ml-kit/migration (accessed Apr. 07, 2024).
[^13]:A. Howard et al., “Searching for MobileNetV3,” arXiv.org, 2019. https://arxiv.org/abs/1905.02244
[^14]:N. Donges, “What is transfer learning? Exploring the popular deep learning approach,” Built In, Aug. 25, 2022. https://builtin.com/data-science/transfer-learning
‌[^15]:Google, “Transfer learning with a pretrained ConvNet | TensorFlow Core,” TensorFlow. https://www.tensorflow.org/tutorials/images/transfer_learning
[^16]:Code academy, “Intro to OpenAI API: Intro to OpenAI GPT API Cheatsheet,” Codecademy. https://www.codecademy.com/learn/intro-to-open-ai-gpt-api/modules/intro-to-open-ai-gpt-api/cheatsheet