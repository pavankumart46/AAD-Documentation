## Installing the Development Environment

### System Requirements:

### Before downloading and installing Android Studio, the following requirements are essential.

- Operating System Version - Microsoft Windows 7/8/10 (32-bit or 64-bit).

- Random Access Memory (RAM) - Minimum 4 GB RAM and 8 GB RAM recommended.

- Free Disk Space - Minimum 4 GB and 8 GB recommended.

- Minimum Required JDK Version - Java Development Kit (JDK) 8.

- Minimum Screen Resolution - 1280 * 800.resolution

### Download and Install Android Studio

#### Step 1

To download the Android Studio, visit the official Android Studio website in your web browser.

#### Step 2

Click on the ["Download Android Studio"](https://developer.android.com/studio?hl=es) option.

#### Step 3

Double click on the downloaded "Android Studio-ide.exe" file.

![step3](https://user-images.githubusercontent.com/21328787/85978184-cf0eb980-b9fb-11ea-82db-501198ec7b1e.jpg)

#### Step 4

"Android Studio Setup" will appear on the screen and click "Next" to proceed.

![step4](https://user-images.githubusercontent.com/21328787/85981155-57dc2400-ba01-11ea-9220-015c4965ade3.jpg)

#### Step 5
 
Select the components that you want to install and click on the "Next" button.

![multilink](https://user-images.githubusercontent.com/21328787/85981396-c8834080-ba01-11ea-81ca-54576a42a141.jpg)

#### Step 6

Now, browse the location where you want to install the Android Studio and click "Next" to proceed.
 
![multilink](https://user-images.githubusercontent.com/21328787/85981399-c91bd700-ba01-11ea-9939-dbe2bd0b3019.jpg)

#### Step 7

Choose a start menu folder for the "Android Studio" shortcut and click the "Install" button to proceed.
 
![multilink](https://user-images.githubusercontent.com/21328787/85981400-c9b46d80-ba01-11ea-8ea4-ff9198240b0d.jpg)

#### Step 8

After the successful completion of the installation, click on the "Next" button.
 
![multilink](https://user-images.githubusercontent.com/21328787/85981402-ca4d0400-ba01-11ea-9d59-a018b8ca78ba.jpg)

#### Step 9

Click on the "Finish" button to proceed.
 
![multilink](https://user-images.githubusercontent.com/21328787/85981404-ca4d0400-ba01-11ea-98d5-6ab9bd769bbb.jpg)

Now, your Android studio welcome screen will appear on the screen.

![multilink](https://user-images.githubusercontent.com/21328787/85981405-cae59a80-ba01-11ea-80db-a212d58a3676.jpg)

Android Studio Setup Configuration
 
#### Step 10

"Android Studio Setup Wizard" will appear on the screen with the welcome wizard. Click on the "Next" button.

![multilink](https://user-images.githubusercontent.com/21328787/85981376-c3be8c80-ba01-11ea-9e3d-c75fed70c3c9.jpg)

#### Step 11

Select (check) the "Standard" option if you are a beginner and do not have any idea about Android Studio. It will install the most common settings and options for you. Click "Next" to proceed.
 
![multilink](https://user-images.githubusercontent.com/21328787/85981381-c620e680-ba01-11ea-9918-48a967f92e70.jpg)


#### Step 12

Now, select the user interface theme as you want. (I prefer Dark theme (Dracula) that is most liked by the coders). Then, click on the "Next" button.
 
![multilink](https://user-images.githubusercontent.com/21328787/85981382-c620e680-ba01-11ea-8e55-5c92cf126c28.jpg)

#### Step 13

Now, click on the "Finish" button to download all the SDK components.
 
![multilink](https://user-images.githubusercontent.com/21328787/85981383-c6b97d00-ba01-11ea-980c-1b1494b9d1f4.jpg)

And, the downloading and installation process of components gets started.
 
![multilink](https://user-images.githubusercontent.com/21328787/85981384-c7521380-ba01-11ea-9fb7-6ccd895873f6.jpg)

#### Step 14

After downloading all the necessary components, click on the "Finish" button.
 
![multilink](https://user-images.githubusercontent.com/21328787/85981390-c7eaaa00-ba01-11ea-8ef4-e303ae2f7260.jpg)

Congrats, your Android Studio has been successfully installed in your system and you can start a new Android studio project.

### Emulator Creation:

![mobile](https://user-images.githubusercontent.com/21328787/85983392-10579700-ba05-11ea-83d0-8196957d6113.png)

  1.	Click on the “Create Virtual Device” button.

![mobile](https://user-images.githubusercontent.com/21328787/85983370-09308900-ba05-11ea-8640-51e62ba6e3c2.jpg)

 2.	Select “Phone” or “Tablet” as Category and select the device which you want to use to make a
Virtual Device. Then click on the “Next” button. Note: select a small screen device for better emulator performance. Devices with a large screen will have a longer launch time (Nexus 4, Nexus 5 etc).

![mobile](https://user-images.githubusercontent.com/21328787/85983372-0a61b600-ba05-11ea-81f2-cfbb2ac7f663.jpg)

 3.	Select the System Image i.e. the API level of Android OS (KitKat, Lollipop etc). Foxit Quick PDF Library for Android requires an API level of 15 or higher.

![mobile](https://user-images.githubusercontent.com/21328787/85983374-0afa4c80-ba05-11ea-8a66-963a6035736e.jpg)

 4.	Now you will see options to verify the Emulator Settings otherwise you may change the settings according to your requirement from this dialog as well and then click on the “Finish” button.
 
![mobile](https://user-images.githubusercontent.com/21328787/85983376-0b92e300-ba05-11ea-9559-d4e204b3e5de.jpg)
 
 5.	Now you will see the newly created Emulator in the list of available Android Virtual Devices.

![mobile](https://user-images.githubusercontent.com/21328787/85983379-0c2b7980-ba05-11ea-92d5-bf65ead738d3.jpg)

 6.	After launching the Emulator (by double-click on the Emulator option that you want to use as show in the screenshot above), wait for the “Home Screen” to load on the Android Virtual Device and then run the application. It’s important that the Virtual Device has finished loading before you try to run the application otherwise it won’t be recognized by Android Studio and you will be prompted to launch the Emulator again which can cause issues. Once the Virtual Device has loaded and you have run the application the dialog below will appear and you can select the
 
Android device that you wish to use.

![mobile](https://user-images.githubusercontent.com/21328787/85983383-0c2b7980-ba05-11ea-81e3-7542dd164437.jpg)

 7.	Finally you should now see your application running in the Android Emulator.

### Notes:

 1.	Android Studio can be a bit sensitive with the Emulators. If you find the Emulator isn’t working
 
(when it has previously worked) check the task manager and remove any loaded Emulator processes. If that doesn’t work try rebooting. This can be an issue in step 7 if you try loading the same Emulator twice you will find that it a) doesn’t let you and b) causes ongoing issues until you have resolved the conflict (as already mentioned, rebooting helps but is not the most efficient).

 2.	We suggest launching the Emulator first from the ADV Manager and waiting for the Emulator to fully load the device (i.e. homescreen is shown) before trying to run the app on the Emulator. If the Emulator has not fully loaded then it will not be shown in the Choose Device screenshot shown in step 7 when you try running the app and then it will give you the option to launch the Emulator again and this will just result in frustrating Emulator conflict issues.


### Enable USB Debugging

 1.	Go to [Settings] > [About Phone] and click [Version] / [Build number] for 7 times in a row to enter developer mode.
 
![mobile](https://user-images.githubusercontent.com/21328787/85983384-0cc41000-ba05-11ea-91ed-7628cad4eced.png)

Go to [Settings] > [Additional Settings] > [Developer Options], you'll be asked to enter a code then press Use.

Toggle to green to enable [Developer Options].To Turn off off Developer options.


Just press the orange highlight at the topmost part of the homescreen.
 
![mobile](https://user-images.githubusercontent.com/21328787/85983385-0d5ca680-ba05-11ea-9417-6c54cf1448be.png)

Reconnect your phone to the PC
Reconnect your phone to the PC with a cable and click the notification on your phone "Transferring Photos via USB."
