---
layout: default
title: Requirements
tab:
    - Project Background
    - Project Objectives
---
# Project Background and Partner Introduction

NTT Data UK Limited, a leading IT services provider, identified challenges faced by junior field engineers in diagnosing and troubleshooting router issues. To address this, NTT Data engaged our team to develop an innovative augmented reality (AR) application to assist their junior engineers.

NTT Data UK Limited is a provider of IT services, having clients across various industries. With a strong focus on delivering reliable technologies and amazing customer service, NTT Data has established itself as a trusted partner for businesses seeking to upscale their technology.
# Project Goals

The primary goal of this project is to develop an AR application that assists junior engineers with the ability to diagnose router issues. The application aims to provide real-time analysis and accurate identification of router LED patterns. Moreover, the app will feature a video conferencing solution in case the junior engineer needs further guidance from a senior engineer for complex issues.

Furthermore, the project aims to(as an optional goal) utilize OpenAI's GPT-4 language model to provide maintenance suggestions based on identified router issues, offering valuable guidance to engineers.

# Requirement Gathering

After evaluating the different methods of capturing requirements, we decided to conduct a semi-structured interview as it allows us to go in-depth and probe where necessary. Below are two sample responses, one each from the Junior Telecom field engineer and the Senior Telecom field engineer.

## Junior Telecom Field Engineer

**What does your troubleshooting routine look like?**

I interview the user to understand the problem, conduct a physical inspection to ensure secure connections, review router settings via the web interface. I also analyze Wi-Fi signal strength in different areas and check and update the firmware if needed.

**What do you typically do when a solution is not apparent to you?**

Typically, I research common problems in Wi-Fi routers through online resources, forums, and knowledge bases. If a solution is still not apparent, I seek guidance from experienced colleagues or supervisors.

**What software features would improve your productivity on the job?**

The app should give step-by-step guidance in real-time, accurately recognize router models to offer tailored advice, and allow for quick access to manuals and guides.  A feature to communicate with senior colleagues using a video link will also be very useful.

## Senior Telecom Field Engineer

**Could you tell me about your job, and how long you have been doing it?**

I have been a senior telecom field engineer for several years, gaining expertise in various telecom technologies and equipment, such as routers, switches, and optical fibers. I primarily manage and train a team of junior field engineers and respond to complicated onsite calls.

**How do you help your junior engineers diagnose complex issues?**

I share troubleshooting methods and offer insights on common telecom issues and effective resolution approaches.  I also provide hands-on training by working alongside junior engineers during complex tasks.

**What software features would improve your productivity?**

In an AR app for field engineers, key features include instant equipment identification, network visualization, remote help via video link, and step-by-step guides for quick problem-solving.
# Personas
<img src="/2023/group43/assets/images/Requirements/Persona_Ryan_Telecom.png" width="750" height="500">

**Junior Telecom Field engineer (Ryan Telecom)**

Ryan, a 25-year-old junior telecom engineer, tackles on-site Wi-Fi issues. Routine repair and diagnostic tasks are easy for Ryan, but complex problems necessitate senior engineer support or equipment return to the company. His company smartphone aids in internet searches and communication.

To boost his efficiency and independence, Ryan desires a user-friendly mobile app for identifying telecom equipment types and offering guided troubleshooting. Reliability and resource efficiency are vital for frequent use without battery concerns. This tool would empower Ryan to independently resolve more telecom equipment issues.

<img src="/2023/group43/assets/images/Requirements/Persona_Maxwell.png" width="750" height="500">

**Experienced Telecom Field engineer (Maxwell Signalton)**

Maxwell, a 40-year-old senior telecom engineer, leads a team of junior engineers and performs complex onsite repairs. Junior engineers often rely on him for guidance due to their limited technical knowledge. He has a company smartphone.

To boost productivity and reduce his onsite visits, Maxwell seeks user-friendly software for junior engineers to independently diagnose and repair equipment. The software should identify equipment, offer troubleshooting steps, and enable live video viewing and annotation, fostering proactive learning.

# Use Case diagram
<img src="/2023/group43/assets/images/Requirements/Use_Case_Diagram_Systems.png" width="750" height="900">

# Use Case List

| ID | Actor | Use Case |
| --- | --- | --- |
| UC1 | Junior Engineer | Barcode Scanning |
| UC2 | Junior Engineer | Object Detection |
| UC3 | Junior Engineer | AR Assistance |
| UC4 | Junior Engineer | Access Router Manual |
| UC5 | Junior Engineer | Suggestive Maintenance |
| UC6 | Junior Engineer | Join Meeting |
| UC7 | Junior Engineer | Access Video Conferencing Manual |
| UC8 | Senior Engineer | Start Meeting |
| UC9 | Senior Engineer | Access Video Conferencing Manual |

# Use Case Descriptions

| Field | Description |
| --- | --- |
| ID | UC1 |
| Actor | Junior Engineer |
| Use Case | Barcode Scanning |
| Description | The junior engineer can scan the barcode of a router to retrieve model information using MLKits barcode scanning capability. |
| Main Flow | <ol><li>Open app</li><li>Click Junior Engineer</li><li>Open the drop-down box at the bottom of the screen</li><li>Select barcode scanning</li><li>Point the camera towards the barcode</li></ol> |
| Result | Barcode Scanning enabled |

| Field | Description |
| --- | --- |
| ID | UC2 |
| Actor | Junior Engineer |
| Use Case | Object Detection |
| Description | The junior engineer can use the ML Kit’s AR capabilities to identify and label different router components based on the tensor flow lite model. |
| Main Flow | <ol><li>Open app</li><li>Select Junior Engineer</li><li>Open the drop-down box at the bottom of the screen</li><li>Select Object recognition</li><li>Point the camera towards the router’s ports</li></ol> |
| Result | Gain an overview and insight into the router features. |



| Field | Description |
| --- | --- |
| ID | UC3 |
| Actor | Junior Engineer |
| Use Case | AR Assistance |
| Description | The junior engineer receives augmented reality assistance for diagnosing issues with routers. |
| Main Flow | <ol><li>Open app</li><li>Select Junior Engineer</li><li>Select from varying AR options</li></ol> |
| Result | AR assistance enabled |

| Field | Description |
| --- | --- |
| ID | UC4 |
| Actor | Junior Engineer |
| Use Case | Access Router Manual |
| Description | The junior engineer can access digital router manuals for troubleshooting purposes. |
| Main Flow | <ol><li>Open app</li><li>Select Junior Engineer</li><li>Select the manual icon located on the top right</li></ol> |
| Result | Router manual opened |

| Field | Description |
| --- | --- |
| ID | UC5 |
| Actor | Junior Engineer |
| Use Case | Suggestive Maintenance |
| Description | The junior engineer receives AI-driven suggestions for maintenance based on the diagnosed router issues. |
| Main Flow | <ol><li>Open app</li><li>Select Junior Engineer</li><li>Open the drop-down box at the bottom of the screen</li><li>Select AI suggestions</li><li>Take a picture of the router</li><li>Submit a picture</li></ol> |
| Result | Gain a detailed analysis and suggestions on how to fix the router issue. |

| Field | Description |
| --- | --- |
| ID | UC6 |
| Actor | Junior Engineer |
| Use Case | Join Meeting |
| Description | The Junior engineer can join an ongoing video conference meeting within the app. |
| Main Flow | <ol><li>Open app</li><li>Select Junior Engineer</li><li>Click the call button on the top-right of the screen</li></ol> |
| Result | An open meeting with a senior engineer will be joined immediately |

| Field | Description |
| --- | --- |
| ID | UC7 |
| Actor | Junior Engineer |
| Use Case | Access Video Conferencing Manual |
| Description | The Junior engineer can access a manual that provides guidance on using the video conferencing features of the app. |
| Main Flow | <ol><li>Open app</li><li>Click the button on the top right with the question mark symbol</li></ol> |
| Result | The video conferencing manual opens |

| Field | Description |
| --- | --- |
| ID | UC8 |
| Actor | Senior Engineer |
| Use Case | Start Meeting |
| Description | The senior engineer can start a new video conference meeting within the app. |
| Main Flow | <ol><li>Open app</li><li>Select Senior Engineer</li></ol> |
| Result | A new meeting started, with the senior engineer as moderator and a random meeting name saved on the database. |

| Field | Description |
| --- | --- |
| ID | UC9 |
| Actor | Senior Engineer |
| Use Case | Access Video Conferencing Manual |
| Description | The Senior engineer can access a manual that provides guidance on using the video conferencing features of the app. |
| Main Flow | <ol><li>Open app</li><li>Click the button on the top right with the question mark symbol</li></ol> |
| Result | The video conferencing manual opens |



# Moscow List(Functional)

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


# Moscow List(Non-Functional)


| ID | Requirement | Priority | Status |
| --- | --- | --- | --- |
| 1 | The application must render AR elements and respond to user interactions within 2 seconds. | Must Have | ✅ |
| 2 | Video conferencing must support at least 480p resolution. | Must Have | ✅ |
| 3 | The app should have less than 0.1% crash rate. | Must Have | ✅ |
| 4 | All user data must be encrypted in transit and at rest. | Must Have | ✅|
| 5 | The system should support concurrent video calls and database operations as user base grows. | Should Have | ✅ |
| 6 | UI/UX should follow best practices for accessibility and ease of use. | Should Have | ✅ |
| 7 | Comprehensive documentation for maintenance and extending the app's capabilities. | Should Have | ✅ |
| 8 | Automatically adjust video quality based on internet bandwidth. | Could Have | ✅ |
| 9 | Allow users to personalize settings, such as notification preferences or theme colors. | Could Have | ❌ |
| 10 | No development for platforms other than Android at this stage. | Won't Have | ❌ |
| 11 | Fully automated fix implementations without human confirmation are not planned. | Won't Have | ❌ |
| 12 | Integration with standalone AR headsets or glasses is not included. | Won't Have | ❌ |