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

```java
public class ObjectDetectorProcessor extends VisionProcessorBase<List<DetectedObject>> {

  private static final String TAG = "ObjectDetectorProcessor";

  private final ObjectDetector detector;

  public ObjectDetectorProcessor(Context context, ObjectDetectorOptionsBase options) {
    super(context);
    detector = ObjectDetection.getClient(options);
  }

  @Override
  public void stop() {
    super.stop();
    detector.close();
  }

  @Override
  protected Task<List<DetectedObject>> detectInImage(InputImage image) {
    return detector.process(image);
  }

  @Override
  protected void onSuccess(
      @NonNull List<DetectedObject> results, @NonNull GraphicOverlay graphicOverlay) {
    for (DetectedObject object : results) {
      graphicOverlay.add(new ObjectGraphic(graphicOverlay, object));
    }
  }

  @Override
  protected void onFailure(@NonNull Exception e) {
    Log.e(TAG, "Object detection failed!", e);
  }
}
```

## Barcode Scanning

This is a secondary feature of our application. It allows the junior engineer to _scan the barcode behind the router, which fetches the router's serial number_. This serial number is then used to fetch the router's details from the database. The code for this feature is present in the `com.example.arapprouterjava/junior/java/barcodescanner` package, with `BarcodeScannerProcessor.java` as the main file, and `BarcodeScanningGraphic.java` as its dependency. The two classes in this package follow a similar structure to the Object Detector feauture, with the `BarcodeScannerProcessor.java` being responsible for processing the barcode, and the `BarcodeScanningGraphic.java` for creating overlays on the detected barcode.

```java
public class BarcodeScannerProcessor extends VisionProcessorBase<List<Barcode>> {
  private static final String TAG = "BarcodeProcessor";

  private final BarcodeScanner barcodeScanner;

  public BarcodeScannerProcessor(Context context, @Nullable ZoomCallback zoomCallback) throws IOException {
    super(context);
//     Note that if you know which format of barcode your app is dealing with, detection will be
//     faster to specify the supported barcode formats one by one, e.g.
     new BarcodeScannerOptions.Builder()
         .setBarcodeFormats(Barcode.FORMAT_QR_CODE)
         .build();
    if (zoomCallback != null) {
      BarcodeScannerOptions options =
          new BarcodeScannerOptions.Builder()
              .setZoomSuggestionOptions(new ZoomSuggestionOptions.Builder(zoomCallback).build())
              .build();
      barcodeScanner = BarcodeScanning.getClient(options);
    } else {
      barcodeScanner = BarcodeScanning.getClient();
    }
  }

  @Override
  public void stop() {
    super.stop();
    barcodeScanner.close();
  }

  @Override
  protected Task<List<Barcode>> detectInImage(InputImage image) {
    return barcodeScanner.process(image);
  }

  @Override
  protected void onSuccess(
      @NonNull List<Barcode> barcodes, @NonNull GraphicOverlay graphicOverlay) {
    if (barcodes.isEmpty()) {
      Log.v(MANUAL_TESTING_LOG, "No barcode has been detected");
    }
  }

  @Override
  protected void onFailure(@NonNull Exception e) {
    Log.e(TAG, "Barcode detection failed " + e);
  }
}
```

## User Manual

This is a complementary feature of our application. _It provides a wide selection of user manual for the junior engineer to select from and displays them as a readable pdf, which guides him/her on how to solve router issues_. The code for this feature is present in `com.example.arapprouterjava/junior/java/preference/ManualPage.java`, this code is mainly responsible of displaying the pdf file, given its path. The pdf files are stored in the `app/assets/user_manuals` folder, and we fetch them using the `AssetManager` class.

```java
public class ManualPage extends AppCompatActivity implements AdapterView.OnItemSelectedListener {
    PDFView pdfView;
    private final List<String> manual_names = new ArrayList<>();
    private static final String TAG = "INFO";
    private final List<String> manual_paths = new ArrayList<>();
    private final Hashtable<String, String> manuals = new Hashtable<>();

    @Override
    protected void onCreate (Bundle savedInstanceState) {
        try {
            loadManuals();
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
        super.onCreate(savedInstanceState);
        setContentView(R.layout.manual_page);
        Spinner spinner = findViewById(R.id.spinner_manual);



        // Creating adapter for spinner
        ArrayAdapter<String> dataAdapter = new ArrayAdapter<>(this, R.layout.spinner_style, manual_names);
        // Drop down layout style - list view with radio button
        dataAdapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item);
        // attaching data adapter to spinner
        spinner.setAdapter(dataAdapter);
        spinner.setOnItemSelectedListener(this);
    }

        private void loadManuals() throws IOException {
        AssetManager assets = getAssets();
        String[] path_list = assets.list("user_manuals");
        assert path_list != null;
        for (String manual: path_list) {
            String manual_name = manual.substring(0, manual.length()-4);
            manual_names.add(manual_name);
            manual_paths.add(manual);
            manuals.put(manual_name, manual);
        }
    }
}
```

There is also a "spinner", which is a selector at the bottom of the page, which allows the user to select the diffrerent manuals. This code is also present in the `ManualPage.java` file.
```java
    @Override
    public synchronized void onItemSelected(AdapterView<?> parent, View view, int pos, long id) {
        String selected = parent.getItemAtPosition(pos).toString();
        pdfView = findViewById(R.id.pdfView);
        Log.println(Log.INFO,TAG,"Selected Manual: " + selected);
        pdfView.fromAsset("user_manuals/"+ selected +".pdf")
                .enableSwipe(false)
                .swipeHorizontal(true)
                .enableDoubletap(true)
                .defaultPage(0)
                .pageFitPolicy(FitPolicy.WIDTH)
                .enableAntialiasing(true)
                .spacing(0)
                .load();
    }

    @Override
    public void onNothingSelected(AdapterView<?> parent) {
        // Do nothing
    }
```


## Call for Help

This is a complementary feature of our application. It allows the junior engineer to _call for help in case he/she is unable to solve the router issue_. There are some conditions necessary for this feature to work:

- The junior engineer must have some type of connectivity/way to access internet to make a video call
- There must be an open meeting present in Jitsi, which the junior engineer can join
The code for this feature is present in the `com.example.arapprouterjava/junior/java/LivePreviewActivity.java` file on line 235-262. This code is responsible for joining into any open meeting in Jitsi, otherwise it return a message saying "No meetings available, please try again later". More information about how the _call procedure_ works can seen in [Video Conferencing](#video-conferencing).


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
