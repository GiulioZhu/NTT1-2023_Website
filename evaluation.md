---
layout: default
title: Evaluation
---
# Summary of Achievements
| Id | Requirement | Priority | Status |
| --- | --- | --- | --- |
| 1 | An Augmented Reality (AR) capable Android application | MUST | ✅ |
| 2 | Identify router features and apply appropriate labels over them | MUST | ✅ |
| 3 | Video conferencing with high quality video feed, call controls, and screen sharing | MUST | ✅ |
| 4 | Access router manuals from the application | MUST | ✅ |
| 5 | Detect router issues based on diagnostic LED light | MUST | ✅ |
| 6 | Recognise router model using barcode scanning | MUST | ✅ |
| 7 | Suggest possible fixes for router issues | COULD HAVE | ✅ |
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
Based on the completed functionalities, the application is able to detect router features, apply labels, initiate video conferencing, access router manuals, detect router issues, and recognise router models and suggests possible fixes for router issues.

In all, the app is functional and meets the requirements set out in the project proposal. We give ourselves Good for functionality.

**Stability**
There were issues in terms of testing and deployments in terms of Unit Testing, Integration Testing and Deployment. We have conducted unit tests for each module and integration tests for the whole application. However, we were not able to debug issues.

There is room 

**Efficiency**
Performance and efficiency has been a key part of our concerns throughout the project cycle. This is a major reason why we adopted Swift as our main development language. Throughout our development process, we used Instrument, a profiler made for iOS applications to keep track of the network and CPU load of our application. When there is an improvement can be made, as stated in the Multi-Threading and Task Queueing section, we made our best effort to utilise technologies we have to make it faster. We also adopted predictive pre-fetching and pre-loading techniques to flatten the network curve. All these measures are worthwhile as we present you our performance testing results, which is 100% faster than similar applications, taking half its time to perform most actions.

We think we have done a good job and give ourselves Very Good for these optimisations done due to efficiency concerns.

**Compatibility**
As this project started with Swift 5, we considered certain aspects of backwards compatibility to make sure we can run our application on relatively older devices. For newer features, we used #available tag provided in Swift to optionally activate some of them when they are supported. However, due to design, implementation and time frame concerns, we were not able to rewrite some parts of our application to make it backwards compatible to iOS 11.0-. We conducted testing with past 3 OS images on our CI platform, Travis. However, it slows down our deployment process significant if we conduct tests on all platforms. Therefore, we can only limit it to 3. There are definitely work can be done to enhance support for much older devices, e.g. iPhone 6, iPod Touch 6 and iPad 4. Given the fact we don't have these devices and the simulator doesn't support older OSes, we would have to limit our support devices to those compatible with iOS 12.0+ and ideal ones to iOS 13.0+.

There are definitely rooms for improvement on this aspect and we give ourselves Good for backwards compatibility.

**Maintainability**
The code base overall is well-documented and can be extended easily as long as it conforms to our interface. We utilised multiple Design Patterns to make sure our code is highly cohesive and loosely coupled. Each module is thoroughly unit-tested and guaranteed to work on its own. Our client has been well informed of the code base from a technical perspective and fully understands how each module work together as an application.

Given the code being well-maintained, we recognise our work as Very Good from a maintainability point of view.

**Project Management**
We only have 2 members in the team. This has both its advantage and disadvantages. Although we have one less person to work with, our teams saves a lot of communication and synchronising effort. We were able to communicate easily and quickly without having schedule a specific time to meet up. As mentioned earlier, we utilised GitHub's issue tracker for this type of basic project management and archived good result. Every team member is clear when it comes up what to do and what are the next steps. Eventually, we are able to finish ahead of our schedule and put some extra effort into optimisations, as well as licensing issues. Retrospectively, we could have used Jira which makes the management process clearer yet more complicated. We are not sure if Jira would make the process better overall.

Our team had a well managed project and we give ourselves Very Good for project management.

# Future Work #
If we had more time, we would have liked to implement the following features:
- Barcode Scanner feature allows the user to open the specific manual related to the product scanned.
- Improvements on the router detection ML model to increase accuracy.
- Improving the router manual UI to make it more readable and user-friendly.