---
layout: default
title: Testing
---

# Testing Strategy #
Our team approached Testing using a combination of Unit Testing, Integration Testing, and UI Testing. We used JUnit with Mockito framework for Unit Testing and Espresso for UI Testing. However, there were many challenges in the testing process due to the complexity of the application, and we were not able to finalize the testing process.

# Unit  Testing #
Because our app heavily relied on the interactions between different objects, we decided to use JUnit with Mockito framework for Unit Testing, because it allowed us to mock the objects and test the interactions between them. We created a test class for each class in the app, and we tested the methods in each class, however, there were a lot of bugs in the process, and after long sessions of troubleshootings with no improvements, we decided to focus on other features as we were not able to finalize the testing process.

# UI Testing #
For the UI testings, recorded Espresso tests were used. We created a test class for each activity in the app, and we tested the interactions between the different views in the app. Our tests covered all the pages of the app and the interactions between them, with all tests passing successfully for API version 30 to 34.
