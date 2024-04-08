---
layout: default
title: Implementation
---

# Main Technologies

As shown in our research, we decided to use `Android Studio` as our IDE with Java as its language.

<img src="/2023/group43/assets/images/implementation/Android_Studio.png" width="200" height="200">

# Dependencies and Tools

# Features

## Router Detection

This is the main feature of our application. By scanning over the routers, it detects the physical components of them, and gives appropriate labels. On the labels, it states the name of the component, and the accuracy of the detection. This feature can be segmented into 2 distinct units:

- **Object Dector Processor**: Using the camera to _scan object, create overlays on the detected components, and label them accordingly_. The code for this feature is present in the `com.example.arapprouterjava/junior/java/objectdetector` package, with `ObjectDetectorProcessor.java` as the main file, and `ObjectGraphic.java` as its dependency. The two classes in this package are responsible for processing and giving labels to the detected objects. However, without an actual ML model to work with, this feature is incomplete. For instance, it can create overlays on the detected objects, but it cannot label them.
- The second unit is the **ML model** itself. This model is responsible for recognizing the physical components of the router. In our project, this model is trained separately following the Transfer Learning method, using the MobileNetV2 model, and is the imported into our project in the `app/assets/custom_models/MobileNetV2_transfer_learning.tflite`.

The main code for connecting these 2 units is present in the 'LivePreviewActivity.java' file. from line 346-356. This code basically loads the recognition model for the detector, so that camera can correctly detected and label the router.

## Barcode Scanning

This is a secondary feature of our application. It allows the junior engineer to _scan the barcode behind the router, which fetches the router's serial number_. This serial number is then used to fetch the router's details from the database. The code for this feature is present in the `com.example.arapprouterjava/junior/java/barcodescanner` package, with `BarcodeScannerProcessor.java` as the main file, and `BarcodeScanningGraphic.java` as its dependency. The two classes in this package follow a similar structure to the Object Detector feauture, with the `BarcodeScannerProcessor.java` being responsible for processing the barcode, and the `BarcodeScanningGraphic.java` for creating overlays on the detected barcode.

## User Manual

This is a complementary feature of our application. _It provides a wide selection of user manual for the junior engineer to select from and displays them as a readable pdf, which guides him/her on how to solve router issues_. The code for this feature is present in `com.example.arapprouterjava/junior/java/preference/ManualPage.java`, this code is mainly responsible of displaying the pdf file, given its path. The pdf files are stored in the `app/assets/user_manuals` folder, and we fetch them using the `AssetManager` class.

## Video Conferencing

In order to implement video conferencing I choose to use the Jitsi SDK and to store these meetings I choose to use the Firebase real-time database.

Senior engineer side:

Overall Flow:

Located in the ActivitySenior.java class. When the senior activity is launched, the Firebase database reference is initialised and the local broadcast manager is initialised. Then the onCreate function is first run, which initially set up the content view which is defined in the specified XML file. Then a function is run to set up the broadcast receiver(details explained below). Then the meeting name is initialised(details below). Finally, the launch Jitsi function is called to launch the meeting.

Random Name Generation:

- In order to implement Random Name generation, I had to `import java.util.Random` and a function that chooses 4 random characters from the string "0123456789qwertyuiopasdfghjklzxcvbnm".

Broadcasting:

- Android apps can send or receive broadcast messages from the Android system and other Android apps, similar to the publish-subscribe design pattern. These broadcasts are sent when an event of interest occurs.
- In order to first set up the broadcasting, an instance of the local broadcast manager is needed, which you get from the `androidx.localbroadcastmanager.content.LocalBroadcastManager` class. An instance of the local broadcast manager is also initiatlised as earlier said.
- Then using the `android.content.IntentFilter`class, we define a few intents we are filtering for that could be broadcasted from the app: “CONFERENCE_JOINED”, “CONFERENCE_TERMINATED”, and “PARTICIPANT_LEFT”. These are defined through Jitsi SDK’s `org.jitsi.meet.sdk.BroadcastEvent` class, which contains predefined broadcast intents. Register these filters into the broadcaster receiver class through the broadcast manager class.
- We have also overridden the onReceive method to define what should happen when a broadcast event happens. Basically, when a broadcast is received an instance of the broadcast receiver is created. This is also where the `android.content.Intent`class is used to identify the intent sent from the broadcast. In the case of the trio broadcasts “CONFERENCE_JOINED”, “CONFERENCE_TERMINATED”, and “PARTICIPANT_LEFT”, we extract the meeting URL from the broadcast, as the information in these broadcasts is defined using hashmaps we must use the class`java.util.HashMap` to extract the meeting URL and get the meeting name using the extract URL function(which just parses and extracts the meeting name through the ‘/’ character). The function `updateMeetingParticipants()` is then called in the case the conference is terminated or the function `writeNewMeeting()` is called when the conference is created, however, the Firebase database is directly updated when a participant leaves as we do not want the handling of conference terminated and participant left to clash with their handling in the junior engineer side of things. The details of these functions are described in the Firebase section.
- We are also required to unregister the receiver in the `onDestroy()` method in order to avoid data leaks.

Calling the Jitsi SDK to start a meeting:

- In order to start a Jitsi meeting, there are a few repositories and imports required:
    - The repositories required within the setting.gradle file are as follows:
        - `google(),`
        - `mavenCentral()`
        - `maven **{**    url "https://github.com/jitsi/jitsi-maven-repository/raw/master/releases"}`
        - `maven **{**    url "https://maven.google.com/"`
        - `maven **{** url 'https://www.jitpack.io/' **}**`
    - The dependency required for the Jitsi SDK is:
        - `implementation('org.jitsi.react:jitsi-meet-sdk:9.0.0') **{** transitive = true **}**`
    - The classes required for Jitsi Meet Activity and my implementation of the Jitsi SDK are:
        - `org.jitsi.meet.sdk.JitsiMeet;`
        - `org.jitsi.meet.sdk.JitsiMeetActivity;`
        - `org.jitsi.meet.sdk.JitsiMeetConferenceOptions;`
- To actually start and create a meeting from the senior engineer side, I created a function called `launchJitsi()`. First of all, specify the server URL that the meeting will be hosted on, then initiate the JitsiMeet builder, which allows you to add options and feature flags such as enabling PiP mode and allowing video to be off when you join a meeting. Then the call was made to the JitsiMeetActivity to launch the meeting from this class.

Adding Firebase:

- The dependencies required to add Firebase are(within the build.gradle(Module):
    - `implementation platform('com.google.firebase:firebase-bom:32.8.0')`
    - `implementation 'com.google.firebase:firebase-firestore:24.11.0'`
    - `implementation("com.google.firebase:firebase-database")`
    - `implementation 'com.google.firebase:firebase-analytics'`
    - `implementation("com.google.firebase:firebase-storage")`
- The required plugin(within the build.gradle(Module)):
    - `plugin: 'com.google.gms.google-services'`
- The required classes(within the activity) are:
    - `com.google.firebase.database.DataSnapshot`
    - `com.google.firebase.database.DatabaseError`
    - `com.google.firebase.database.DatabaseReference`
    - `com.google.firebase.database.FirebaseDatabase`
    - `com.google.firebase.database.ValueEventListener`
- First as mentioned before the Firebase database reference is initialised. There are two main functions that handle updating the Firebase database: `updateMeetingParticipants()` and `writeNewMeeting()`. In the case of a conference joined the `writeNewMeeting()` function is called, this function takes two parameters, meeting name and the number of participants in the meeting. The function declares the Firebase instance and connects it to a specified database through a URL. Then using the specific meeting name creates a new meeting key and stores the participants as value(in this case is 1) to set up a new meeting. The `updateMeetingParticipants()` takes in the parameter meeting name and declares the database in the same way. The code listens for a single value event on a node in the Firebase Realtime Database, identified by the meeting name. When the data at the node changes, the `onDataChange()` method is triggered. Inside `onDataChange()`, the code retrieves the current value of the node as an Integer and stores it in the data variable. The code then decrements the data value by 1, indicating a participant has left the meeting. If the decremented data value is 0, it means no more participants in the meeting, and the code removes the entire node associated with the meeting name. In the case of the senior engineer leaving, this is updated from the junior engineer side of the code to avoid clashes. In the case of “PARTICIPANT_LEFT”, the value is directly updated when handling the if cases for the broadcasting, in order to avoid clashes with the “CONFERENCE_TERMINATED” and “PARTICIPANT_LEFT” broadcasts in the junior activity. If the decremented data value is neither 0 nor 1, it logs an error message. The `onCancelled()` method handles errors that might occur during the database operation.

Junior engineer side

Note: The repositories, dependencies, and classes I have mentioned for the senior engineer side are exactly the same, thus I will not mention them again.

Overall Flow:

Located in the LivePreviewActivity.java class. When the call button is clicked, the junior activity is launched, the Firebase database reference is initialised and the local broadcast manager is initialised. Then the `onCreate()` function is first run, which initially set up the content view which is defined in the specified XML file. Then a function is run to set up the broadcast receiver(details explained below). The app then queries the database and looks for an open meeting, if there are no open meetings a toast message is displayed that says “Please try again later”. The code establishes a connection to the Firebase Realtime Database through the unique URL in the `onCreate()` function and retrieves a reference to the "Meetings" node. When the call button is clicked, it adds a listener for a single value event on the "Meetings" node. Inside the `onDataChange()` method, the code iterates through all children (meetings) under the "Meetings" node. For each meeting, it extracts the number of participants. If a meeting has exactly one participant, the code retrieves the meeting name and launches the Jitsi video conferencing session with that name. If no meeting with one participant is found, the code displays a Toast message indicating no available meetings. The `onCancelled` method handles any errors occurring during the database operation.

Broadcasting:

- Here the implementations of each of the broadcasts “CONFERENCE_JOINED” and “PARTICIPANT_LEFT” are slightly different from the senior activity and there is no implementation for “COMFERENCE_TERMINATED” as this is updated in the senior engineer side of the code. “CONFERENCE_JOINED” and PARTICIPANT_LEFT” both call `updateMeetingPartcipants()`but the implementation of this function is slightly different here. The data again is decremented. If the participants are now 0 the node is removed but if the participants are 1(meaning a junior engineer is left in the call) a hang-up broadcast is sent to the Jitsi meeting to close the meeting for the junior engineer and remove the meeting node from the database. When the conference is joined, however, the database is updated directly to 2 as the junior engineer will always be the second to join the meeting.

Calling the Jitsi SDK to start a meeting::

- Same as in the senior engineer section

Adding Firebase:

- Extra details are described in the broadcasting section


## Camera source and model selection:

```java
private void createCameraSource(String model) {
    // If there's no existing cameraSource, create one.
    if (cameraSource == null) {
      cameraSource = new CameraSource(this, graphicOverlay);
    }

    try {
      switch (model) {
        case ROUTER_DETECTION:
          LocalModel customlocalModel =
                  new LocalModel.Builder()
                          .setAssetFilePath("custom_models/MobileNetV2_transfer_learning.tflite")
                          .build();

          CustomObjectDetectorOptions newcustomObjectDetectorOptions =
                  PreferenceUtils.getCustomObjectDetectorOptionsForLivePreview(this, customlocalModel);
          cameraSource.setMachineLearningFrameProcessor(
                  new ObjectDetectorProcessor(this, newcustomObjectDetectorOptions));

          break;

        case OBJECT_DETECTION_CUSTOM:
          Log.i(TAG, "Using Custom Object Detector Processor");
          LocalModel localModel =
              new LocalModel.Builder()
                  .setAssetFilePath("custom_models/tf_lite_model1.tflite")
                  .build();

            CustomObjectDetectorOptions customObjectDetectorOptions =
                    PreferenceUtils.getCustomObjectDetectorOptionsForLivePreview(this, localModel);
            cameraSource.setMachineLearningFrameProcessor(
                    new ObjectDetectorProcessor(this, customObjectDetectorOptions));

          break;
        case BARCODE_SCANNING:
          Log.i(TAG, "Using Barcode Detector Processor");
          ZoomCallback zoomCallback = null;
          if (PreferenceUtils.shouldEnableAutoZoom(this)) {
            zoomCallback = zoomLevel -> cameraSource.setZoom(zoomLevel);
          }
          cameraSource.setMachineLearningFrameProcessor(
              new BarcodeScannerProcessor(this, zoomCallback));
          break;

        case AI_SUGGESTIONS:
          Intent intent = new Intent(LivePreviewActivity.this, AiSuggestions.class);
          startActivity(intent);
        default:
          Log.e(TAG, "Unknown model: " + model);
      }

    } catch (RuntimeException | IOException e) {
      Log.e(TAG, "Can not create image processor: " + model, e);
      Toast.makeText(
              getApplicationContext(),
              "Can not create image processor: " + e.getMessage(),
              Toast.LENGTH_LONG)
          .show();
    }
  }
```

The `createCameraSource()`method initialises a camera source if not already initialised. It then uses switch statements for recognising which object detector to initialise based on the user’s selection. For "ROUTER_DETECTION" or "OBJECT_DETECTION_CUSTOM", it sets up a custom object detector using TensorFlow Lite models. For "BARCODE_SCANNING", it configures a barcode scanner. If the model is "AI_SUGGESTIONS", it starts a new activity to receive guidance from a large language model. Any unknown model triggers an error log. Exception handling is included for potential runtime or I/O exceptions during setup, with error messages displayed accordingly.

## AI guidance:

```java
 public void imageChooser() {

        // create an instance of the
        // intent of the type image
        Intent i = new Intent();
        i.setType("image/*");
        i.setAction(Intent.ACTION_GET_CONTENT);

        // pass the constant to compare it
        // with the returned requestCode
        startActivityForResult(Intent.createChooser(i, "Select Picture"), SELECT_PICTURE);
    }
```

The `imageChooser` method sets up an intent to select an image from device storage using `ACTION_GET_CONTENT`. It starts an activity for result, presenting a chooser dialog titled "Select Picture". This method is invoked using an `OnClickListener` when the user presses the select a picture button.

```java
protected void onActivityResult(int requestCode, int resultCode, @Nullable Intent data) {
        super.onActivityResult(requestCode, resultCode, data);

        if (requestCode == SELECT_PICTURE && resultCode == RESULT_OK) {
            ImageView imageView = findViewById(R.id.imageView);
            Uri selectedImageURI = data.getData();
            currentPhotoPath = selectedImageURI.toString();
            imageView.setImageURI(selectedImageURI);
            try {
                Bitmap bitmap = MediaStore.Images.Media.getBitmap(getContentResolver(), selectedImageURI);
                // initialize byte stream
                ByteArrayOutputStream stream = new ByteArrayOutputStream();
                // compress Bitmap
                bitmap.compress(Bitmap.CompressFormat.JPEG, 100, stream);
                // Initialize byte array
                byte[] bytes = stream.toByteArray();
                // get base64 encoded string
                Base64String = Base64.encodeToString(bytes, Base64.DEFAULT);
                // set encoded text on textview

            } catch (IOException e) {
                e.printStackTrace();
            }
        }

    }
}
```

The `onActivityResult` method converts the image selected by the user from their gallery into a base64 format so that it can be sent as a prompt to the GPT 4 vision API. It verifies if the user has successfully selected an image. If successful, it retrieves the URI of the selected image, assigns it to the imageView for display. It also converts the image into a Base64 string using `Base64.encodeToString()` method and stores it as a string in the `base64String` variable.

```java
public void query_gpt(String image_url) throws Exception {
        String url = "{ \"model\": \"gpt-4-vision-preview\", \"temperature\": \"0.2\", \"messages\": [{ \"role\": \"system\", \"content\": [ { \"type\": \"text\", \"text\": \"You are an experienced network engineer that can diagnose issues with routers. Look at the provided image to suggest some possible solutions to restore connectivity. For instance if you spot disconnected power cables or LAN cables suggest that the cables be connected. No lights on the router suggests that it is off so you can suggest that the router be turned on. Blue LED's on the router means that the router is connected to the internet. Use the diagnostic LED colors to inform your suggestions. Give your suggestions in numbered points. If you do not see a router in the image, always output 'please provide a router picture'. If you do not have a suggestion, always output 'please contact a senior engineer for guidance'\"}]},{ \"role\": \"user\", \"content\": [ { \"type\": \"text\", \"text\": \"Whats wrong with the router in the image?\"}, { \"type\": \"image_url\", \"image_url\": { \"url\": \"data:image/jpeg;base64,%s\", \"detail\": \"low\"}}]}], \"max_tokens\": 600}";
        String api_url = String.format(url, image_url.replace("\n", ""));
        JSONObject api_json = new JSONObject(api_url);

        String req_body = String.format(api_url, image_url);
        Request request = new Request.Builder().header("Content-Type", "application/json").addHeader("Authorization", String.format("Bearer %s", BuildConfig.GPT_API_KEY))
                .url("https://api.openai.com/v1/chat/completions").post(RequestBody.create(api_json.toString(), JSON))
                .build();

        client.newCall(request).enqueue(new Callback() {
            @Override
            public void onFailure(Call call, IOException e) {
                e.printStackTrace();
                Toast.makeText(
                                getApplicationContext(),
                                "API request failed" + e.getCause(),
                                Toast.LENGTH_LONG)
                        .show();
            }

            @Override
            public void onResponse(Call call, Response response) {
                try (ResponseBody responseBody = response.body()) {
                    if (!response.isSuccessful()) {
                        Log.e(TAG, "Unexpected code " + responseBody.string());
                        Toast.makeText(
                                        getApplicationContext(),
                                        "Unexpected code " + responseBody.string(),
                                        Toast.LENGTH_LONG)
                                .show();
                    } else {
                        TextView textView = findViewById(R.id.textView1);
                        String res = responseBody.string();
                        JSONObject json = new JSONObject(res);
                        new Handler(Looper.getMainLooper()).post(new Runnable() {
                            @Override
                            public void run() {
                                try {
                                    textView.setText(json.getJSONArray("choices").getJSONObject(0).getJSONObject("message").getString("content"));

                                } catch (JSONException e) {
                                    throw new RuntimeException(e);
                                }
                            }
                        });

                    }
                } catch (Exception e) {
                    throw new RuntimeException(e);
                }
            }
        });
    }
```

This function queries the GPT-4 Vision API with an image URL. It prepares a JSON request containing model details, message instructions, and the image URL. The `okhttp3` library is used to constructs an HTTP request to the API endpoint with the authorisation header and the JSON body. The API keys are loaded from the applications local environment via `BuildConfig.GPT_API_KEY` thereby preventing any misuse of OpenAI API keys. Upon response, it handles both success and failure cases through the `onResponse` and `onFailure` methods respectively. In case of success, it extracts the response text from the JSON and updates a TextView using a `Handler`. The `Handler` is employed to post a `Runnable` to the applications main thread's message queue. This `Runnable` contains the logic to update a `TextView` with the response text received from the API. In case of failure, it logs the error and displays a toast message with the failure details.

```java
btn_gpt.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                try {
                    query_gpt(Base64String);
                } catch (Exception e) {
                    throw new RuntimeException(e);
                }
            }
        });
```

This `OnClickListener` method is invoked when the user clicks on the query button after selecting an image. The Base64 representation of the image store in `Base64String` is passed to the previously discussed `query_gpt` function to get suggestions from the GPT 4 vision large language model.

## TensorFlow transfer learning

```python
mobilenet_v2 = "https://tfhub.dev/google/tf2-preview/mobilenet_v2/feature_vector/4"
inception_v3 = "https://tfhub.dev/google/tf2-preview/inception_v3/feature_vector/4"

feature_extractor_model = mobilenet_v2
```

URL to obtain headless version of the MobileNetV2 model with its classification layer removed.

```python
feature_extractor_layer = hub.KerasLayer(
    feature_extractor_model,
    input_shape=(224, 224, 3),
    trainable=False)
```

Create the feature extractor by wrapping the pre-trained model as a Keras layer with `[hub.KerasLayer](https://www.tensorflow.org/hub/api_docs/python/hub/KerasLayer)`. Use the `trainable=False` argument to freeze the variables, so that the training only modifies the new classifier layer.

```python
num_classes = len(class_names)

model = tf.keras.Sequential([
  feature_extractor_layer,
  tf.keras.layers.Dense(num_classes)
])
```

To complete the model, wrap the feature extractor layer in a `tf.keras.Sequential` model and add a fully-connected dense layer for classification.

```python
NUM_EPOCHS = 30

history = model.fit(train_ds,
                    validation_data=val_ds,
                    epochs=NUM_EPOCHS,
                    callbacks=tensorboard_callback)
```

Model trained for 30 Epochs on the training dataset.

## Convert TensorFlow model to Tflite:

```python
import tensorflow as tf

# Convert the model
converter = tf.lite.TFLiteConverter.from_saved_model("./saved_models/1711509820") # path to the SavedModel directory
tflite_model = converter.convert()

# Save the model.
with open('model.tflite', 'wb') as f:
  f.write(tflite_model)
```

This Python code imports TensorFlow and then converts a TensorFlow SavedModel into a TensorFlow Lite model. It loads the SavedModel from the specified directory, converts it using **`tf.lite.TFLiteConverter`**, and saves the resulting TensorFlow Lite model to a file named "model.tflite".

## Video Conferencing

# Implementation Showcase

{% include view-slideshow.html %}

# Technical Video Demo
