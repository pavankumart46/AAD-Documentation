
# FIREBASE ML KIT FOR ANDROID

Firebase ML Kit is a library that allows you to effortlessly, and with minimal code, use a variety of highly accurate, pre-trained deep models in your Android apps. Most of the models it offers are available both locally and on the Google Cloud.

Currently, the models are limited to computer-vision-related tasks only, such as optical character recognition, barcode scanning, and object detection.

## how to add Firebase ML Kit to an Android Studio project and use some of its base APIs?

## Prerequisites:

Before you proceed, make sure you have access to the following:

•	The latest version of Android Studio 

•	A device or emulator running Android API level 21 or higher

•	A Firebase account

•	A Google Cloud account.

## 1.Create a Firebase Project

To enable Firebase services for your app, you must create a Firebase project for it. So log in to the Firebase console and, on the welcome screen, press the Add project button.

![picture alt](https://github.com/chaitanyak963/Document/raw/master/a(1).png)

•	In the dialog that pops up, give the project a name that's easy to remember and press the Create project button.

![picture alt](https://github.com/chaitanyak963/Document/raw/master/b(1).png)

•	After several seconds, you should see a notification telling you that the new project is ready. Press the Continue button to proceed.

•	In the next screen, go to the Develop section and click on the ML Kit link to see all the services ML Kit offers.

![picture alt](https://github.com/chaitanyak963/Document/raw/master/c(1).png)

•	In this , we'll be using three services: text recognition, face detection, and image labeling. You don't have to take any steps to explicitly enable them if you intend to work with only the local models that come with ML Kit. In this tutorial, though, we'll be using both local and cloud-based models. So click on the Cloud API usage link next.

•	You'll now be taken to the Google Cloud console, where you can simply press the Enable button shown in the Cloud Vision API section to activate the cloud-based models. Note, however, that this will work only if you have billing enabled for your Google Cloud account.

![picture alt](https://github.com/chaitanyak963/Document/raw/master/d(1).png)

## 2.Configure your Android Studio Project

Before you start using the Firebase ML Kit APIs, you must establish a connection between your Android Studio project and the Firebase project you created in the previous step. To do so, open the Firebase Assistant panel by going to Tools > Firebase.

The Firebase Assistant doesn't have any support for ML Kit currently. Nevertheless, by using it to add Firebase Analytics instead, you can still avoid establishing the connection manually. Therefore, expand the Analytics section, click on the Log an Analytics event link, and press the Connect to Firebase button.

In the dialog that pops up, make sure you select the Choose an existing Firebase or Google project option and pick the Firebase project you created.

![picture alt](https://github.com/chaitanyak963/Document/raw/master/e(1).png)

Press the Connect to Firebase button next. At this point, the Assistant will automatically download a google-services.json file, containing API keys and project IDs, and add it to the app module.

After the connection has been established successfully, make sure you press the Add Analytics to your app button to add various core Firebase dependencies to your app module's build.gradle file.

Next, to actually add the ML Kit library, open the build.gradle file and type in the following implementation dependencies:

```
implementation 'com.google.firebase:firebase-ml-vision:16.0.0'
implementation 'com.google.firebase:firebase-ml-vision-image-label-model:15.0.0'
```
•	To simplify the process of downloading images from the Internet and displaying them in your app, I suggest you also add a dependency for the Picasso library.

```
implementation 'com.squareup.picasso:picasso:2.5.2'
```

•	Additionally, add Anko as a dependency to make sure your Kotlin code is both concise and intuitive.

```
implementation 'org.jetbrains.anko:anko-commons:0.10.5'
```
•	By default, Firebase ML Kit's local models are automatically downloaded to your users' devices only when needed. If you want them to be downloaded as soon as your app is installed, however, add the following code to the AndroidManifest.xml file:

```
<meta-data
    android:name="com.google.firebase.ml.vision.DEPENDENCIES"
    android:value="text,face,label" />
```
## 3.Define a Layout

In this , we'll be creating an app that allows users to type in URLs of images and perform text recognition, face detection, and image labeling operations on them. Therefore, the layout of the app must have an EditText widget, where the users can type in the URLs, and three Button widgets, which let them choose which operation they want to perform. 

Optionally, you can include an ImageView widget to display the images.

If you position all the above widgets using a RelativeLayout widget, your layout XML file should like this:

```
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
 
    <EditText
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Image URL"
        android:id="@+id/image_url_field"
        android:imeOptions="actionDone"
        android:inputType="textUri"/>
 
    <ImageView
        android:layout_width="match_parent"
        android:layout_height="300dp"
        android:id="@+id/image_holder"
        android:layout_below="@+id/image_url_field"
        android:layout_marginTop="10dp"
        android:scaleType="centerInside"/>
 
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:layout_alignParentBottom="true">
        <Button
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="0.33"
            android:text="Text"
            android:onClick="recognizeText"/>
        <Button
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            
            android:layout_weight="0.33"
            android:text="Faces"
            android:onClick="detectFaces"/>
        <Button
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="0.33"
            android:text="Labels"
            android:onClick="generateLabels"/>
    </LinearLayout>
 
</RelativeLayout>

```
•	Here's a more visual representation of the layout:

![picture alt](https://github.com/chaitanyak963/Document/raw/master/f(1).png)

•	In the XML above, you may have noticed that each button has an onClick attribute pointing to an on-click event handler method. Those methods don't exist yet, so create them inside your activity now.

```
fun recognizeText(v: View) {
    // To do   
}
 
fun detectFaces(v: View) {
    // To do
}
 
fun generateLabels(v: View) {
    // To do
}
```

## 4.Load an Image

When the user presses the Done key after typing an image's URL into the EditText widget, our app must download the image and display it inside the ImageView widget.

To detect actions performed on the user's virtual keyboard, associate an OnEditorActionListener object with the EditText widget. Inside the listener, after confirming that the IME_ACTION_DONE action was performed, you can simply call Picasso's load() and into() methods to load and display the image respectively.

Accordingly, add the following code inside the onCreate() method of your activity:

```
image_url_field.setOnEditorActionListener { _, action, _ ->
    if (action == EditorInfo.IME_ACTION_DONE) {
        Picasso.with(ctx).load(image_url_field.text.toString())
                .into(image_holder)
        true
    }
    false
}

```
## 5.Recognize Text

Firebase ML Kit has separate detector classes for all the various image recognition operations it offers. To recognize text, you must either use the FirebaseVisionTextDetector class, which depends on a local model, or use the FirebaseVisionCloudTextDetector class, which depends on a cloud-based model. For now, let's use the former. It's far faster, but it can handle text written in the Latin alphabet only.

An ML Kit detector expects its input to be in the form of a FirebaseVisionImage object. To create such an object, all you need to do is call the fromBitmap() utility method of the FirebaseVisionImage class and pass a bitmap to it. The following code, which must be added to the recognizeText() event handler we created earlier, shows you how to convert the image that is being displayed in the layout's ImageView widget into a bitmap, and then create a FirebaseVisionImage object out of it:

```
val textImage = FirebaseVisionImage.fromBitmap(
        (image_holder.drawable as BitmapDrawable).bitmap
)
```

•	Next, to get a reference to a FirebaseVisionTextDetector object, you must use a FirebaseVision instance.
```
val detector = FirebaseVision.getInstance().visionTextDetector
```

•	You can now start the text recognition process by calling the detectInImage() method and passing the FirebaseVisionImage object to it. Because the method runs asynchronously, it returns a Task object. Consequently, to be able to process the result when it is available, you must attach an OnCompleteListener instance to it. Here's how:

```
detector.detectInImage(textImage)
        .addOnCompleteListener {
            // More code here
        }
 ```
 
 •	Inside the listener, you'll have access to a list of Block objects. In general, each block can be thought of as a separate paragraph detected in the image. By taking a look at the text properties of all the Block objects, you can determine all the text that has been detected. The following code shows you how to do so:
 
 ```
 var detectedText = ""
it.result.blocks.forEach {
    detectedText += it.text + "\n"
}
```

•	How you use the detected text is of course up to you. For now, let's just display it using an alert dialog. Thanks to Anko's alert() function, doing so takes very little code.

```
runOnUiThread {
    alert(detectedText, "Text").show()
}
```
In the above code, the runOnUiThread() method ensures that the alert() function is run on the main thread of the application.

Lastly, once you have finished using the detector, you must remember to call its close() method to release all the resources it holds.

 If you run the app now, type in the URL of an image containing lots of text, and press the Text button, you should be able to see ML Kit's text recognition service in action.
 
 
![picture alt](https://github.com/chaitanyak963/Document/raw/master/g(1).png)

ML Kit's local model for text recognition is reasonably accurate with most kinds of printed text.

## 6.Detect Faces:

Even though they don't share any common high-level interface, most of the detector classes have identical methods. That means that detecting faces in an image is not too different from recognizing text. However, note that ML Kit currently offers only a local model for face detection, which can be accessed using the FirebaseVisionFaceDetector class. You can get a reference to an instance of it using the FirebaseVision class.

Add the following code to the detectFaces() method:

```
val detector = FirebaseVision.getInstance().visionFaceDetector
```
By calling the detectInImage() method again and passing a bitmap to it, you can start the face detection process asynchronously. By using an OnCompleteListener instance attached to the Task object it returns, you can easily know when the process is complete.

```
detector.detectInImage(FirebaseVisionImage.fromBitmap(
            (image_holder.drawable as BitmapDrawable).bitmap
        )).addOnCompleteListener {
            // More code here        
        }
```
Inside the listener, you'll have access to a list of FirebaseVisionFace objects, which contain the coordinates of rectangles that circumscribe the detected faces. So let us now draw those rectangles over a copy of the original image that was processed.

To create a copy of the original image's bitmap, you must use its copy() method as shown below:

```
var markedBitmap =
    (image_holder.drawable as BitmapDrawable)
            .bitmap
            .copy(Bitmap.Config.ARGB_8888, true)
```

•	Next, to be able to draw on the new bitmap, you must create Canvas and Paint objects for it. Using a slightly transparent color for the rectangles would be ideal.

```
val canvas = Canvas(markedBitmap)
val paint = Paint(Paint.ANTI_ALIAS_FLAG)
paint.color = Color.parseColor("#99003399")
                            // semi-transparent blue
```

•	At this point, you can simply loop through the list of FirebaseVisionFace objects and use their boundingBox properties to draw rectangles over the detected faces.

```
it.result.forEach {
    canvas.drawRect(it.boundingBox, paint)
}
```

•	Finally, don't forget to pass the new bitmap to the ImageView widget once it's ready.

```
runOnUiThread {
    image_holder.setImageBitmap(markedBitmap)
}
```

•	If you run the app now, you should be able to perform face detection on any image that has people in it.

![picture alt](https://github.com/chaitanyak963/Document/raw/master/h(1).png)


I'm sure you'll be impressed with how fast and accurate ML Kit's face detection operations are.

## 7.Generate Labels

To generate labels for an image, you must use either the local model-based FirebaseVisionLabelDetector class or the cloud model-based FirebaseVisionCloudLabelDetector class. Because we've been using only local models throughout this tutorial, let's use the cloud model now. To get a reference to an instance of the FirebaseVisionCloudLabelDetector class, you must again use the FirebaseVision class.

Add the following code to the generateLabels() method:

```
val detector = 
        FirebaseVision.getInstance().visionCloudLabelDetector
```
•	Next, as usual, call the detectInImage() method and assign an OnCompleteListener instance to its return value.

```
detector.detectInImage(FirebaseVisionImage.fromBitmap(
            (image_holder.drawable as BitmapDrawable).bitmap
        )).addOnCompleteListener {
            // More code here
        }
```

This time, inside the listener, you'll have access to a list of FirebaseVisionCloudLabel objects, each of which has a label property containing a potential label for the image. Each label also has a confidence property associated with it, specifying how sure ML Kit is about the label.

The following code shows you how to loop through the list of labels and generate an alert dialog displaying only those labels whose confidence scores are more than 70%.

```
var output = ""
it.result.forEach {
    if(it.confidence > 0.7)
        output += it.label + "\n"
}
runOnUiThread {
    alert(output, "Labels").show()
}
```

Go ahead and run the app again to see what labels your app generates for the images you throw at it.

![picture alt](https://github.com/chaitanyak963/Document/raw/master/i(1).png)


## Conclusion

With Firebase ML Kit, Google wants to make machine learning as accessible and mainstream as simpler tasks such as analytics and crash reporting. In this introductory tutorial, you learned how to work with some of its base APIs in Android apps. You also learned how to use both the cloud and local models it offers.

