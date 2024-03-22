---
layout: default
title: Research
---
# Related Project Review
Due to the nature of the project, we  decided to conduct a review of the technologies and tools that related to our field. This allowed us to understand the capabilities of the tools and how they can be used to achieve the project goals. Among all of the open source tools, we found [Google AR Core](https://github.com/google-ar/) and [ML Kit](https://github.com/googlesamples/mlkit) to be the most relevant ones. 

## Google AR Core
When we were given the requirements, this was the first tool that came to our minds. **AR Core** is a platform that allows developers to build *augmented reality experiences*. It is available for Android and iOS devices. Among its open source projects, we found [Augmented Images](https://github.com/google-ar/arcore-android-sdk/tree/master/samples/augmented_image_java) and [Camera Sharing](https://github.com/google-ar/arcore-android-sdk/tree/master/samples/shared_camera_java) projects to be the most relevant ones to our case.

**Augmented Images** is a project that allows users to *detect and track images in the real world*. This is a very useful feature for our project as we need to detect and track the labels on the routers. This allows junior engineers to scan for router labels and gather essential information about the routers.

On the other hand, **Camera Sharing** is a project that allows users *to share the camera feed between two devices*. This is a **key feature** for our project as we need a method to establish communication between the junior engineer and the senior engineer. It allows the senior engineer to see what the junior engineer is seeing and guide them through the process.


In the development process with AR Core we found out that AR Core, despite its wonderful features, it *deviated from our vision of the software*. Our app needed **object detections** and **supporting graphic overlays** to display information, which AR Core didn't provide. We also found out compatibility issues with AR Core, which made it difficult to implement the features we wanted. This led us to transition into a more practical tool, ML Kit.

## ML Kit
**ML Kit** is a platform that allows developers to build *machine learning models* and *integrate them into their applications*. It is available for Android and iOS devices. Among its open source projects, we found out that [ML Kit Vision App](https://github.com/googlesamples/mlkit/tree/master/android/vision-quickstart) matches most of our requirements. Some of its most relevant features are: **object detection** and **barcode scanning**. 

**Object Detection** is a feature that allows users to *detect and track objects in the live camera feed*. The detection model is based on a trained ML model, which means that we can train the model to recognize specific features of the routers.

**Barcode Scanning** is a feature that allows users to scan and process barcodes. This is also an important feature in our project, because it's *scalable*. All routers have barcodes, so it's universally applicable. 

It's worth noting that ML Kit is a **more general** tool than AR Core, so it can be used in a wider range of applications. *It's edge over AR Core is that it incorporates multiple features in a single compact app, which best suited our needs*. 


# Technology Review
In the development process, we explored a variety of technologies and ways that could be used to achieve the project goals. 

We considered our project *persona* and *scenario* and we discovered that **mobile development** was the solution. Among it's advantages, we found that it's **scalable**, **portable** and **cost-effective**. Because junior engineers are always on the move, it's important that they *have access to the app at all times*, also it's important that the app is *easy to use* and *doesn't require any additional hardware*. For these reasons, we excluded **tablets** and **ar goggles** from our list of potential solutions.

## Devices

## Algorithms

## Programming Languages

## Frameworks
Among our list of possible frameworks, we considered **Unity**, **Vuforia**, and **Android Studio** as potential solutions. 

## Libraries

## APIs

