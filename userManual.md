---
layout: default
title: User Manual
---
<style>
    .container {
    display: grid;
    align-items: center; 
    grid-template-columns: 1fr 2fr;
    column-gap: 5px;
    }

    img {
    max-width: 100%;
    max-height:100%;
    }

    .text {
    font-size: 20px;
    }
</style>

Here's the user manual for our software. Please review this document before using our software. Please refer to the deployment manual for instructions on how to install our software, as this page only contains instructions on how to use our software.

# Table of Contents
1. [Home](#Home)
2. [Junior Engineer](#Junior-Engineer)

    2.1. [Router Detection](#Router-Detection)

    2.2. [AI Guidance](#AI-Guidance)

    2.3. [Barcode Scanner](#Barcode-Scanner)

3. [Senior Engineer](#Senior-Engineer)

# Home
<html>
  <head>
    <title>Home Page</title>
  </head>
  <body>
    <div class="container">
      <div class="image">
        <img src="/2023/group43/assets/images/implementation/MainActivityView.png">
      </div>
      <div class="text">
        <p>This is the main screen when opening the app. When you first open the app, it will ask for permissions <i>to take pictures and record video, and access photos and medias on the device</i>. It's <strong>mandatory</strong> to allow such permissions, in order to run the app. Otherwise, the app would quit and re-prompt the user for permissions</p>

        <p>There are two main buttons on the page: <strong>Senior Engineer</strong>, <strong>Junior Engineer</strong>. Based on the role of the user, select the appropriate options. For additional in-app guides, feel free to click on the <i>help button</i> at the top right of the page</p>
      </div>
    </div>
  </body>
</html>
<br>

# Junior Engineer
There are a couple of features available for the Junior Engineer. The main features are Router Detection, AI Guidance, and Barcode Scanner, which can be selected at from a spinner (a.k.a. dropdown selection bar) the bottom of the screen. On its side, there is a button to change the camera facing direction. 

Additionally there are a couple of buttons available at the top right of the screen, which serves as secondary tools for the user:
- **Settings**
- **Call**: Joins a room call with an available Senior Engineer
- **User Manual**: Opens a list of user manuals for routers

## Router Detection
<html>
  <head>
    <title>Router Detection</title>
  </head>
  <body>
    <div class="container">
      <div class="image">
        <img src="/2023/group43/assets/images/implementation/JuniorEngineerView.png">
      </div>
      <div class="text">
        <p>Point the camera towards router components like the power switch and various WAN, WLAN ports. The app will create overlays and displays labels on them to help you. </p>
      </div>
    </div>
  </body>
</html>
<br>

## AI Guidance
<html>
  <head>
    <title>AI Guidance</title>
  </head>
  <body>
    <div class="container">
      <div class="image">
        <img src="/2023/group43/assets/images/implementation/AiGuidanceView.png">
      </div>
      <div class="text">
        <p>To use this feature, firstly, the user (junior engineer) has to press the <strong>SELECT A PICTURE</strong> button to upload an image of the router that he's working with. Then, the <strong>QUERY</strong> button will send a request to a generative AI to return some useful guidelines.</p>
      </div>
    </div>
  </body>
</html>
<br>

## Barcode Scanner
<html>
  <head>
    <title>Barcode Scanning</title>
  </head>
  <body>
    <div class="container">
      <div class="image">
        <img src="/2023/group43/assets/images/implementation/BarcodeScanning.png">
      </div>
      <div class="text">
        <p>Point the camera towards the barcodes at the back of the router. The app will create overlays and displays labels on them to help you. Usually, the barcodescans will return the serial number and the MAC number of the routers. If the serial number matches with the one in the firebase database, a button will pop out, and when pressed, it redirects the user to the router's specific user manual page.</p>
      </div>
    </div>
  </body>
</html>
<br>

# Senior Engineer
The Senior Engineer has a different set of features compared to the Junior Engineer. The main feature is the ability to host a meating room for the Junior Engineer to join. The user plays a more passive role and awaits for the Junior Engineer to join the room.
<html>
  <head>
    <title>Senior Engineer</title>
  </head>
  <body>
    <div class="container">
      <div class="image">
        <img src="/2023/group43/assets/images/implementation/SeniorEngineerView.png">
      </div>
      <div class="text">
        <p>The user can <i>set his name, and change his audio and video settings</i> prior to starting a video call.</p>
      </div>
    </div>
  </body>
</html>
<br>

<html>
  <head>
    <title>Meeting View</title>
  </head>
  <body>
    <div class="container">
      <div class="image">
        <img src="/2023/group43/assets/images/implementation/MeetingView.png">
      </div>
      <div class="text">
        <p>This is the UI for the meeting room, the user can <i>mute/unmute his microphone, open/close his camera, open the chat, or explore additional features</i>.</p>
      </div>
    </div>
  </body>
</html>
<br>

<html>
  <head>
    <title>Additional Features</title>
  </head>
  <body>
    <div class="container">
      <div class="image">
        <img src="/2023/group43/assets/images/implementation/MeetingAdditionalFeaturesView.png">
      </div>
      <div class="text">
        <p>Here are all the additional available features. Feel free to explore and experiment with these settings.</p>
      </div>
    </div>
  </body>
</html>
<br>