---
layout: default
title: Evaluation
---
# Summary of Achievements

| Id | Requirement | Priority | Status | Contributors|
| --- | --- | --- | --- |
| 1 | An Augmented Reality (AR) capable Android application | MUST | ✅ | Ahmed, Ayman, Giulio |
| 2 | Identify router features and apply appropriate labels over them | MUST | ✅ |Ahmed |
| 3 | Video conferencing with high quality video feed, call controls, and screen sharing | MUST | ✅ |Ayman  |
| 4 | Access router manuals from the application | MUST | ✅ | Giulio |
| 5 | Detect router issues based on diagnostic LED light | MUST | ✅ | Ahmed |
| 6 | Recognise router model using barcode scanning | MUST | ✅ | Giulio |
| 7 | Suggest possible fixes for router issues | COULD HAVE | ✅ | Ahmed|
| 8 | Use Large language models for information gathering and question answering based on manuals | COULD HAVE | ❌ |

## Individual Contribution ##
{% include individual-contribution.html %}

# Critical Evaluation of the Project #
Down below is a summary of the evaluations of our project from different perspectives.

**User Interface and Experience**
We adopted a similar camera structure UI from other AR applications. This is because we believe this is the most intuitive way to present AR information to users. We also adopted a similar user manual selector to make the app more user-friendly, and intuitive.

We've had the UI and user experience tested by multiple users and received positive feedback. The UI is clean and easy to navigate, and the AR feature is intuitive and user-friendly. The user manual selector is also easy to use and provides a seamless experience for users.

In all, We give ourselves Good for our UI work.

**Functionality**
In relation to the proposed requirements and the Moscow list, we have successfully implemented all the MUST requirements and left out 1 COULD HAVE requirement. 
Based on the completed functionalities, the application is able to detect router features, apply labels, initiate video conferencing, access router manuals, detect router issues, and recognise router models and suggests possible fixes for router issues. Features such as Barcode scanning and router feature detection are functional but further refinement is required to improve them further. 

In all, the app is functional and meets the requirements set out in the project proposal. We give ourselves Good for functionality.

**Stability**
There were issues in terms of testing and deployments in terms of Unit Testing, Integration Testing and Deployment. We have conducted unit tests for each module and integration tests for the whole application. However, we were not able to debug issues.

There is room for improvement in terms of testing and debugging. We give ourselves Fair for stability.

**Efficiency**
In terms of performance, our app runs smoothly and efficiently. We have optimised the app to reduce latency, improve the user experience, and increase the FPS of the camera. We have also optimised the app to reduce memory usage and improve the app's performance.

We think we have done a good job and give ourselves Very Good for these optimisations done due to efficiency concerns.

**Compatibility**
As this project started with Android API 30, we have made sure that our app is compatible with Android API 30 and above. We have also tested the app on multiple devices to ensure compatibility. However, we have not tested the app on older devices and cannot guarantee compatibility with older devices.

There are definitely rooms for improvement on this aspect and we give ourselves Good for compatibility.

**Maintainability**
The code base overall is documented and can be extended easily as long as it conforms to our interface. We utilised some Design Patterns to make sure our code is highly cohesive and loosely coupled. We have provided comments and deployment manual for future developers to understand the codebase and deploy the app.

Given the code being well-maintained, we recognise our work as Good from a maintainability point of view.

**Project Management**
Our team was able to communicate easily and quickly throughout Whatsapp and Teams, and collaboratively worked on Github. Every team member is clear about his own tasks. Eventually, we are able to finish the requirements and deliver the project on time.

Our team had a well managed project and we give ourselves Very Good for project management.

# Future Work #
If we had more time, we would have liked to implement the following features:
- Taking pictures directly from camera and querying them through GPT instead of selecting an image.
- Barcode Scanner feature allows the user to open the specific manual related to the product scanned.
- Improvements on the router detection ML model to increase accuracy.
- Improving the router manual UI to make it more readable and user-friendly.
- Automatic PiP mode when screen-share button is clicked for the junior engineer.