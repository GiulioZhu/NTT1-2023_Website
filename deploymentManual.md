---
layout: default
title: User Manual
---
Here's the deployment manual for our software. This contains instructions on how to install our software and how to extend on its features.
# Table of Contents
1. [Pre-Requisites](#Pre-Requisites)
2. [Installation](#Installation)
3. [Build and Run](#Build-and-Run)

# Pre-Requisites
- Git
- Android Studio Hedgehog (2023.1.1) or later versions. (Our latest used version: Iguana 2023.2.1)
- Devices running Android API 26+ version or a Device Simulator with similar specs (ideally API 30 above)

# Installation
To install our software, please follow the steps below (if you have access to our repository at https://github.com/Ahmed-Ansari02/COMP0016-NTT1-2023-.git):
```bash
git clone https://github.com/Ahmed-Ansari02/COMP0016-NTT1-2023-.git
```
or access to our github repository at https://github.com/Ahmed-Ansari02/COMP0016-NTT1-2023-.git and download the zip file.
![Github Page](/2023/group43/assets/images/appendix/Github_page.png)

# Add OpenAI API key:
1. Create an OpenAI API account
2. Navigate to the API key page and "Create new secret key".
3. Go to local.properties file of the cloned repository and add GPT_API_KEY = YOUR_API_KEY. *YOUR_API_KEY* should be the API key obtained from the last step.

# Build and Run #
1. Open Android Studio and at the top of the page select `File` > `Open File or Project` and select the folder where you cloned the repository. (To know if you selected the correct folder, the selected folder should have an android icon on the left side of the folder name)
![Open Project](/2023/group43/assets/images/appendix/Importing_folder.png)
2. Wait for the project to build and sync with Gradle. If you see a pop-up at the bottom right of the screen, click on `Sync Now`.
3. You should also configure an AVD (Android Virtual Device) to run the app. To do this, look for `Device Manager` tab at the right of the app
    3.1. Click on `+ Create Virtual Device` and select a device that has an API level of 26 or above. Click `Next` and `Finish` to create the device.
    3.2. Alternatively, you can use your own android device and pair it using wifi or USB cable.
![Device Manager](/2023/group43/assets/images/appendix/Device_Manager.png)
4. Click on the green play button at the top right of the screen to run the app.


