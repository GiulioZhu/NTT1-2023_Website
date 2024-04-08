---
layout: default
title: Research
---

# Related Project Review

Due to the nature of the project, we decided to conduct a review of the technologies and tools that related to our field. This allowed us to understand the capabilities of the tools and how they can be used to achieve the project goals. Among all of the open source tools, we found [Google AR Core](https://github.com/google-ar/) and [ML Kit](https://github.com/googlesamples/mlkit) to be the most relevant ones.

## Google AR Core

When we were given the requirements, this was the first tool that came to our minds. **AR Core** is a platform that allows developers to build _augmented reality experiences_. It is available for Android and iOS devices. Among its open source projects, we found [Augmented Images](https://github.com/google-ar/arcore-android-sdk/tree/master/samples/augmented_image_java) and [Camera Sharing](https://github.com/google-ar/arcore-android-sdk/tree/master/samples/shared_camera_java) projects to be the most relevant ones to our case[^1].

**Augmented Images** is a project that allows users to _detect and track images in the real world_. This is a very useful feature for our project as we need to detect and track the labels on the routers. This allows junior engineers to scan for router labels and gather essential information about the routers.

On the other hand, **Camera Sharing** is a project that allows users _to share the camera feed between two devices_. This is a **key feature** for our project as we need a method to establish communication between the junior engineer and the senior engineer. It allows the senior engineer to see what the junior engineer is seeing and guide them through the process.

In the development process with AR Core we found out that AR Core, despite its wonderful features, it _deviated from our vision of the software_. Our app needed **object detections** and **supporting graphic overlays** to display information, which AR Core didn't provide. We also found out compatibility issues with AR Core, which made it difficult to implement the features we wanted. This led us to transition into a more practical tool, ML Kit.

## ML Kit

**ML Kit** is a platform that allows developers to build _machine learning models_ and _integrate them into their applications_. It is available for Android and iOS devices. Among its open source projects, we found out that [ML Kit Vision App](https://github.com/googlesamples/mlkit/tree/master/android/vision-quickstart) matches most of our requirements. Some of its most relevant features are: **object detection** and **barcode scanning**[^2].

**Object Detection** is a feature that allows users to _detect and track objects in the live camera feed_. The detection model is based on a trained ML model, which means that we can train the model to recognize specific features of the routers.

**Barcode Scanning** is a feature that allows users to scan and process barcodes. This is also an important feature in our project, because it's _scalable_. All routers have barcodes, so it's universally applicable.

It's worth noting that ML Kit is a **more general** tool than AR Core, so it can be used in a wider range of applications. _It's edge over AR Core is that it incorporates multiple features in a single compact app, which best suited our needs_.
‌

# Technology Review

In the development process, we explored a variety of technologies and ways that could be used to achieve the project goals.

We considered our project _persona_ and _scenario_ and we discovered that **mobile development** was the solution. Among it's advantages, we found that it's **scalable**, **portable** and **cost-effective**. Because junior engineers are always on the move, it's important that they _have access to the app at all times_, also it's important that the app is _easy to use_ and _doesn't require any additional hardware_. For these reasons, we excluded **tablets** and **ar goggles** from our list of potential solutions.

## Devices

Our client gave us the freedom to choose Android or IOS as the operating system for our application. Since we were aiming moderately complicated application, we aimed to build a native phone application as it would be more performant and allow us to easily leverage native APIs to access device features[^3]. Therefore, we planned to employ either _Java_ or _Swift_ when developing our application instead of cross platform UI libraries such as _React native_ or _Flutter_.

Both the Android SDK and IOS SDK provided all the necessary tooling and APIs that we needed to fulfil the client requirements. For instance, one of our main objectives was to use a custom machine learning model to detect router features and attach labels to objects for which Android’s _ML kit_ and IOS’s _Core ML_ would suffice. Furthermore Android and IOS both had excellent documentation, third party library support and large and active developer communities that ensured that we could efficiently and quickly implement features and resolve bugs.

Our final decision came down to the devices readily available to us for development and the choice of programming language used with each operating system’s SDK.

Two out of three teammates were using Android devices which would allow them to quickly download the app to their devices and test its functionality - something we needed to do quite often with an App that scanned the environment using the camera and viewfinder. Furthermore, for native IOS development a relatively modern apple(Mac OS) computer is required to install the _Xcode IDE_ to develop applications[^4]. Since our team had 2 Windows machines and 1 Macbook, we decided it would be wise to develop an Android application since all our devices were capable of running Android Studio and thus we could independently develop features of our app. Android studio also has built in support for emulators which can be used to see how code changes reflect in our application in real time.

Android development is done primarily in Java/Kotlin[^5] while IOS development is done in Apple’s Swift programming language[^6]. As our team had previous experience working with Java due to our university module, we decided to opt for Android development as it would involve less of a learning curve than learning a completely new programming language such as Swift (and its associated Swift UI framework). This ensured we could quickly dive into the development process and start implementing features. Due to Google’s deep involvement with the Android project, we also received the benefit of deep integration within Google’s ecosystem of technologies such as Firebase[^7] and Tensorflow[^8]. This made it relatively straight forward for us to implement these technologies in our application.

## Algorithms

A core feature of our application was to recognise Router features and apply labels over them. To achieve this, a custom machine learning model capable of recognising these features was needed. _ML kit_, the machine learning framework native to our Android application, required a _Tensorflow lite model_ for object detection which we had to create using the Tensorflow machine learning framework[^9].

To train a machine learning model We initially planned to use Firebase ML SDK. Although this service would have simplified the training process, it is primarily geared towards cloud hosted models and Google recommends using ML kit SDK for our target features of Object detection and Barcode scanning[^10].

For the machine learning model architecture we opted for _MobileNetV2_ which is convolutional neural network tuned to work on resource constrained devices such as mobile and IOT[^11]. Its streamlined architecture enables swift inference, crucial for real-time object detection applications on phones. Despite its compact size, MobileNetV2 maintains competitive accuracy, ensuring reliable performance without burdening the device's hardware. This is particularly beneficial for mobile applications where responsiveness and battery life are paramount. We also considered architectures such as MobileDET, Yolo and SSD (Single Shot Multibox Detector) however despite the speed and accuracy advantages over MobileNet, their relative complexities and higher resource requirements made them less suited for our use case.

We had the option of training the MobileNetV2 model from scratch but that would entail a long training period due to the computing resources at our disposal. There was also the risk of creating a less accurate model due to our limited training data. We therefore opted for a transfer learning approach of creating our custom model[^12]. For this we downloaded a headless version of the MobileNetV2 model with the final classification layer removed, which we fine tuned on our dataset of router features. This approach ensured that our model could take advantage of the existing model’s learned feature and removing the need to start from scratch by training an entirely new model[^13]. By only training the newly-added classifier layers and freezing layers of the base model, transfer learning provided us a way to quickly create an accurate model in an efficient manner.


## Programming Languages
### Introduction

Due to the specific nature of our project, we wanted to build a native phone application as it would be easier to implement AR and ML functionalities with native APIs. Thus we had three choices regarding programming language: Java/Kotlin, C#, and Swift.

C# was developed by Microsoft as part of its .NET initiative. It is an object-oriented language that is widely used. As it can be used for mobile development through the game engine Unity, it became a choice for our app’s programming language. Furthermore, C# is known for its performance in game development and AR capabilities(through various SDKs), due to the Unity game engine, which provides a multitude of tools for high-performance applications. As already mentioned, C# is integrated with the .NET platform, an open-source platform for developing apps. The C# ecosystem is made up of two main parts: the Common Language Runtime(CLR) and the .NET class library. The CLR is a runtime environment that manages the execution of .NET programs and provides services such as memory management, type safety, exception handling, garbage collection, and security [^17]. The CLR also includes the Just-In-Time compiler that converts intermediate code into native machine code, this process allows for high-performance .NET applications to be made and codes written in different programming languages to seamlessly work together [^18]. However, the .NET class library is a comprehensive, object-oriented collection of reusable types that can be used to develop applications ranging from GUI and CLI applications to applications based on [ASP.NET](http://ASP.NET) for web and networked applications [^19].

Similarly, Java is a high-level, class-based, object-oriented language that facilitates the write-once, run-anywhere approach due to its ability to minimize dependencies. This means that Java applications, once compiled to bytecode, can run on any platform that supports Java [^20]. Java's architecture is integral to its WORA capability and consists of three primary parts: the **Java Virtual Machine(JVM)**, the **Java Runtime Environment(JRE)**, and the **Java Development Kit(JDK)[^21]**. The JVM is the main reason for Java's platform independence. This is because it is responsible for executing the code generated by Java compilers by interpreting bytecode to machine code, allowing Java applications to run on any platform. The JVM also includes garbage collection and JIT compilation to produce high-performance applications. The JRE includes the JVM, core libraries, and other components necessary to run Java applications, thus essentially acting as a container that provides everything Java applications need to run on any device. The JDK is the superset of the JRE and includes all the tools necessary for the development of a Java application, for example, the compiler javac, the archiver jar, and the interpreter java among others. Overall, it is the JDK that allows the creation of Java applications that can be executed and run by JRE and JVM.

Swift is a compiled programming language designed for iOS and macOS. It supports a multi-paradigm approach, incorporating object-oriented, functional, and imperative programming styles. Swift is particularly proficient in terms of security, safety, and error handling. Due to its protocol-oriented programming style, it has a flexible and reusable code structure. It is known for its clean syntax and high performance through its well-designed memory management. Its main components are the **Swift Compiler**, the **Swift Runtime**, the **Swift Standard Library,** the **Swift Package Manager**, **Xcode,** and **Playgrounds[^22]**. The Swift compiler translates Swift code into an intermediate representation(IR). The compiler then optimises the code then the LLVM(Low-Level Virtual Machine) backend of the compiler converts the code to machine code for the target architecture. It is worth mentioning that the LLVM is a widely used open-source compilation framework. Swift uses Automatic Reference Counting(ARC) for memory management, which controls the memory lifecycle of objects and class instances for example, frees up memory when a class instance is no longer needed. The Swift Standard library provides the fundamental classes for data types, algorithms, and utilities. The official tool for managing the distribution of Swift Code, the Swift Package manager can automate the process of linking, downloading, and compiling dependencies. Xcode is Apple’s IDE for macOS, it provides the tools to develop software for the Apple platform. Its components include the Swift Compiler, the interface builder, and other tools for the development of iOS and macOS applications. Playgrounds, however, is the interactive development environment that allows code to be written and executed immediately to see results, mainly used for learning Swift or prototyping.

### Comparison of Tooling

Our requirement for a native app makes it clear that for Java we would need to use Android Studio, for C# we would have to use the Unity game engine(as we need to build an AR app), and for Swift, we would need to use Xcode. To decide which programming language we wanted to use, we needed to delve deeper into how we could accomplish an AR app using these specific languages. Thus, we will go through the possibilities to make a comparison:

Firstly, for C# it would be required that the Unity Game engine with the AR Foundation framework be used. The AR Foundation framework is an abstraction layer over ARCore and ARKit, which allows cross-platform AR development. “The AR Foundation package contains interfaces for AR features but doesn't implement any features itself. To use AR Foundation on a target platform, you also need a separate *provider plug-in* package for that platform.”[^23] The plug-in packages mentioned are the SDKs ARCore and ARKit. Unity’s ML agents also allowed the incorporation of machine learning detection into AR. C#’s ability to deploy AR applications on both Android and iOS from a single codebase means that it has cross-platform capabilities.

Secondly, for Java, the development of an AR app would involve using Android Studio, Google's official Integrated Development Environment (IDE) for building Android apps. Android Studio also provides native support for ARCore, Google's platform for building AR functionalities on Android devices.

ARCore offers essential features for creating AR functionalities, such as motion tracking, environmental understanding, and light estimation. It uses Java, along with the Android SDK and NDK (Native Development Kit), to enable developers to create AR apps that can integrate virtual objects into the real world. Java's libraries, frameworks, and tools for Android development can further aid in the AR app development process, including third-party AR SDKs and libraries specifically designed for AR development on Android.

For Swift, however, the development of an AR app would use Xcode, Apple's IDE for building apps for iOS, macOS, watchOS, and tvOS. Xcode provides native support for ARKit, Apple's framework for creating augmented reality experiences on iOS devices.

ARKit also allows for motion tracking, scene understanding, and realistic rendering of virtual objects. Swift, being Apple's modern programming language can be integrated with ARKit and other Apple frameworks. Additionally, Swift's focus on performance and safety features can be advantageous for computationally intensive AR applications. Furthermore, Apple’s developer tools, resources, documentation, and sample projects can aid in the development of AR apps using Swift and ARKit.

Considering the requirement for a native AR app that can potentially target both Android and iOS platforms, C# with Unity may be the most suitable choice. It provides a cross-platform solution with the AR Foundation framework, allowing you to develop the AR app once and deploy it to multiple platforms. Additionally, Unity's game engine and 3D capabilities can be advantageous for creating immersive AR experiences.

### Comparison of Performance

<img src="/2023/group43/assets/images/Research/Performance_Comparison.png" width="750" height="500">

Figure 1: Speed Comparison of different programming languages

When it comes to general performance, C#, Java, and Swift have their own strengths and weaknesses. The benchmark compares the performance of various programming languages, including C# at 209.36 ms, Java at 600.98 ms, and Swift at 141.23 ms, in calculating π through the Leibniz formula 10,000,000 times. This specific benchmark shows that for this mathematical computation task, Swift outperforms both C# and Java, with C# being faster than Java but slower than Swift, the results are shown in Figure 1.

However, platform-specific optimizations can play a significant role in the performance of AR applications. Languages like Swift and Java may benefit from platform-specific optimizations and native APIs, which could improve their performance in AR applications targeted for those platforms. These optimizations can use the hardware and software architectures, providing better resource utilization and improving aspects like rendering performance, sensor data processing, and memory management.

Hardware acceleration is another important factor that can impact the performance of AR applications. The ability to use hardware acceleration through APIs like Metal, on iOS, or Vulkan, on Android, can significantly boost performance for graphics-intensive tasks in AR applications. These APIs allow developers to take advantage of low-level hardware features, such as GPUs, for good rendering and computation, which is essential for delivering smooth AR experiences.

Third-party libraries and frameworks for AR development can also affect the overall performance of the application. The availability and quality of these libraries and frameworks can impact various aspects of AR application development, such as computer vision. Also, libraries can compensate for potential performance differences between programming languages, allowing developers to utilise the strengths of each language.

Thus, strictly based on the benchmark data, marking the general performance of these programming languages, in terms of performance the best option seems to be Swift.

While benchmark data provides insights into the general performance characteristics of programming languages, it does not necessarily translate directly to how these languages will perform in the context of AR applications. Factors such as platform-specific optimizations, hardware acceleration, third-party libraries, and developer expertise play crucial roles in determining the overall performance and user experience of AR applications.

### Conclusion

While tooling and performance are important factors to consider, the decision was made based off of the team's familiarity and resources available. Two members of the team had Windows laptops, so coding in Swift would be very difficult as it is for Apple's ecosystem. Additionally, with two members having Android phones, testing an AR application developed in Swift would be difficult, as it is primarily targeted for iOS devices.

Furthermore, the team's prior experience with Java eliminates the time wasted on the learning curve associated with learning a new language like Swift or C#. As the team had existing knowledge in Java, we could streamline the development process and minimize delays.

Therefore, we choose Java as our language.
## Frameworks

Among our list of possible frameworks, we considered **Unity**, **Vuforia**, and **Android Studio** as potential solutions.

**Unity** is a cross-platform engine that allows developers to build _3D and 2D games, apps, and experiences for entertainment, film, automotive, architecture, and more_. It uses C# and C++, and it supports a variety of platforms, including android and ios[^15]. It provides a robust and intuitive development environment, which is beginner-friendly and efficient for experienced developers. It also boasts of an extensive asset store contributed by the Unity community offering a wide range of completed assets to work with which simplifies the development process. It also allows performance optimization with its built-in tools, which ensures smooth performance across devices[^16].

**Vuforia** is a scalble AR content creation solution that transforms existing 3D CAD or product for mobile devices that enables the creation of augmented reality applications. Some of its features include _image targets, cloud recognition service, and barcode scanners_. This allows developers to quickly create recognition models, since cloud recognition service allows developers to upload images to the cloud and get recognition results in real-time without any requirement on training. It also supports a wide range of devices and platforms, including Android, iOS, and UWP and also provides a wide range of APIs and SDKs for developers to work with, which makes it a versatile tool for AR development.

**Android Studio** is the official IDE for Android app development, based on IntelliJ IDEA. It provides a comprehensive development environment for Android app development, with features like _code completion, refactoring, and lint tools_. It also provides a visual layout editor, which allows developers to create layouts by dragging and dropping UI elements. It also provides a wide range of tools for debugging and testing, which makes it a powerful tool for Android app development.

## SDKs
### Research Video Conferencing SDK

WebRTC is an open-source project that provides a set of APIs and protocols for real-time communication over the web. It allows for peer-to-peer communication. WebRTC is also supported natively by modern web browsers, making it easy to integrate into web applications. It offers features such as video/audio streaming, and screen sharing. However, WebRTC requires developers to build their own user interface and handle signaling and connection management, providing flexibility and customization options but requiring more development effort.

On the other hand, Jitsi is an open-source video conferencing platform that utilizes WebRTC technology. It provides a ready-to-use video conferencing solution with a user interface and various features out of the box. Jitsi offers features like screen sharing, recording, live streaming, and support for various audio/video codecs. It has built-in support for secure connections (HTTPS), encryption, and authentication. Jitsi can be self-hosted or used via the public Jitsi Meet service, offering a simplified setup and deployment process compared to building a WebRTC solution from scratch. Additionally, Jitsi has a dedicated community and regular updates, ensuring ongoing support and improvements.

While WebRTC offers flexibility and customization options, it requires more development effort to build a complete video conferencing solution. Jitsi, on the other hand, provides a ready-to-use platform with a user-friendly interface and various features out of the box. Given the requirement for a video conferencing solution, Jitsi emerges as a better choice due to its ease of deployment, feature-rich offering, ongoing support and updates, and faster time-to-market compared to building a custom WebRTC solution from scratch.

### Research Database SDK

Firebase Realtime Database offers real-time data synchronization. This feature ensures that as meetings are created or joined, updates are instantaneously reflected across all connected devices. This real-time capability is essential for enabling junior engineers to quickly find and join meetings without delays. Additionally, Firebase is known for its scalability, automatically adjusting to handle data changes well. This is particularly important for an application that may experience intense usage periods.

Another significant advantage of Firebase is its ease of use. It is known for its user-friendly interface and easy setup process, making it an ideal choice for first-time users or development teams under tight deadlines. The comprehensive documentation and good community support further streamline the development process, allowing for a quicker focus shift to building the app's core features, such as AR detection and video conferencing integration.

While Firebase shines in many areas, it's also important to consider the benefits of using a more traditional database system like PostgreSQL, especially when enhanced with real-time capabilities through extensions. PostgreSQL is a powerful, open-source object-relational database system known for its use with complex queries. When equipped with real-time extensions, PostgreSQL can serve real-time applications by providing instantaneous data updates, similar to Firebase.

However, setting up and managing a PostgreSQL database, even with real-time extensions, tends to be more complex and time-consuming compared to Firebase. This complexity may not be ideal for teams looking to quickly develop and deploy their applications. Additionally, while PostgreSQL offers great scalability, it typically requires more management compared to Firebase's more efficient approach to handling fluctuating loads.

In conclusion, considering the specific needs of the AR app - including real-time updates for meeting information, ease of setup and use, and the ability to scale dynamically - Firebase’s Realtime Database emerges as the superior choice, especially for first-time users and teams prioritizing rapid development and deployment. Its built-in real-time capabilities ensure that the application can efficiently manage the dynamic nature of meeting data. Firebase's ease of integration and management allows developers to focus on enhancing the app's core functionalities, making it the best option for this project.

## APIs

### OpenAI GPT 4 vision API
For our AI guidance feature we converted a user selected image into base64 and then sent the query to the _GPT 4 vision API_. The API response would then be displayed to the user in the text view. We set the model _temperature_ to zero and made use of prompt engineering techniques to prevent the large language model from hallucinating or demonstrating unpredictable behaviour[^14].

## Summary of Technical Decisions
In summary we have decided to opt with Android development, using Android Studio with the Java programming language. For the video conferencing solution, we've opted to use the Jitsi meet SDK and Firebase realtime database to store the meetings. Furthermore, we choose to use MLKit for our object-detection, barcode scanning functionality, and to provide overlays. We also used the ChatGPT API in order to detect errors and give predictive maintenance.


<!-- i will add a comparison table here - Giuli, link: https://www.w3schools.com/howto/howto_css_comparison_table.asp -->

# References
[^1]: “AR Core,” Google Developers. https://developers.google.com/ar.
[^2]: “ML Kit,” Google Developers. https://developers.google.com/ml-kit.
[^3]: P. Manager, “Native App vs Cross-Platform: How to Make a Choice,” JatApp, Feb. 20, 2019. https://jatapp.co/blog/.
[^4]: Apple, “Xcode - Support - Apple Developer,” Apple.com, 2020. https://developer.apple.com/support/xcode/top-advantages-of-using-unity-for-game-development-bd64b6a3004native-or-cross-platform-app-development/ (accessed Apr. 07, 2024).
[^5]: Apple, “Swift,” Apple. https://www.apple.com/lae/swift(accessed Apr. 07, 2024).
[^6]: Google, “Kotlin and Android,” Android Developers. https://developer.android.com/kotlin.
[^7]: Google, “Add Firebase to your Android project Firebase," Firebase, 2019. https://firebase.google.com/docs/android/setup.
[^8]: Google, “Custom Models with ML Kit,” Google Developers. https://developers.google.com/ml-kit/custom-models.
[^9]: Google, “TensorFlow Lite guide,” TensorFlow. https://www.tensorflow.org/lite/guide.
[^10]: Google, “Migration guide ML Kit,” Google for Developers. https://developers.google.com/ml-kit/migration (accessed Apr. 07, 2024).
[^11]: A. Howard et al., “Searching for MobileNetV3,” arXiv.org, 2019. https://arxiv.org/abs/1905.02244.
[^12]: N. Donges, “What is transfer learning? Exploring the popular deep learning approach,” Built In, Aug. 25, 2022. https://builtin.com/data-science/transfer-learning.
[^13]: Google, “Transfer learning with a pretrained ConvNet TensorFlow Core,” TensorFlow. https://www.tensorflow.org/tutorials/images/transfer_learning.
[^14]: Code academy, “Intro to OpenAI API: Intro to OpenAI GPT API Cheatsheet,” Codecademy. https://www.codecademy.com/learn/intro-to-open-ai-gpt-api/modules/intro-to-open-ai-gpt-api/cheatsheet.
[^15]: Unity Technologies, “Unity - Unity,” Unity, 2019. https://unity.com.
[^16]: X. Web, “Top Advantages of Using Unity for Game Development,” Medium, Jun. 19, 2023. https://medium.com/@xceltecweb/.
‌[^17]: Wikipedia, ".NET Framework," [Online]. Available: https://en.wikipedia.org/wiki/.NET_Framework. [Accessed: 23-Mar-2024]
[^18]: Microsoft, "What is .NET Framework?," [Online]. Available: https://dotnet.microsoft.com/en-us/learn/dotnet/what-is-dotnet-framework. [Accessed: 23-Mar-2024]

[^19]: Microsoft, ".NET Documentation," [Online]. Available: https://docs.microsoft.com/en-us/dotnet/. [Accessed: 23-Mar-2024]

[^20]: Wikipedia Contributors, “Java (programming language),” [Online] *Wikipedia*, Mar. 29, 2019. https://en.wikipedia.org/wiki/Java_%28programming_language%29 [Accessed: 23-Mar-2024]

[^21]:  “Java Architecture and its Components  JVM, JRE, and JDK,” [Online] *Edureka*, Jul. 25, 2019. https://www.edureka.co/blog/java-architecture/ [Accessed: 23-Mar-2024]

[^22]: Apple Inc., "Swift Programming Language," Apple Developer Documentation, 2023. [Online]. Available: https://developer.apple.com/swift/. [Accessed: Mar. 23, 2024]

[^23]: “AR Foundation  AR Foundation  5.1.0-pre.2,”[Online] *docs.unity3d.com*. https://docs.unity3d.com/Packages/com.unity.xr.arfoundation@5.1/manual/index.html [Accessed: Mar. 23, 2024]