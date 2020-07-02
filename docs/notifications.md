# Notifications 
### What is a notification ?
A notification is a message that Android displays outside your app's UI to provide the user with reminders, communication from other people, or other timely information from your app. 
<img src="notfication.png" height=200dp>

### Why is a notification ?
* To notify the user if there is trigger of the data from the background services.
* It let the user to know about the messages or any updates about the applications along with the actions.
* User may know about the triggers without going into the application.
* Also will send the live changes like temperature ,time ,date and location.

### History of Notification :
* This Notifications are started from the android version 4.4 (Kitkat).
* For every new version released there is a much evaluation in the design,style,text ,icons for the notification.
* It becomes more effective and efficient for the user to work with it.
* Now it is also coming with the notifications dots to make use have the fast interaction with the applications easily.

### How is a Notification ?
* Notification is created and build using the Notification Service,Notification Manager and Notification Compat.
* Upto Android version 7 (Nougat) all this tools are same but from the Android version 8 (Oreo) a new built in tool is introduced and named as Notification Channel under the Android Jetpack Components.
###### Building a notification upto Android 7(Nougat) :
```
NotificationManager manager = (NotificationManager)getSystemService(NOTIFICATION_SERVICE );
 NotificationCompat.Builder builder = new NotificationCompat.Builder(this)
           .setSmallIcon(R.drawable.android_icon)
           .setContentTitle("You've been notified!")
           .setContentText("This is your notification text")
	.setPriority(NotificationCompat.PRIORITY_HIGH);
manager.notify(ID,builder.build());
```
###### Building a notification for above Android 8(Oreo) :
```
 if (android.os.Build.VERSION.SDK_INT >= android.os.Build.VERSION_CODES.O) {
            NotificationChannel channel = new NotificationChannel("Cherry","APSSDC",
                    NotificationManager.IMPORTANCE_HIGH);
            channel.enableLights(true);
            channel.enableVibration(true);
            channel.setLightColor(Color.GREEN);
            manager.createNotificationChannel(channel);
        }
```
#### Importance level and priority contraints :
* Below table represents the imporatance levels and contraints for Android 7(& Below) and Android 8(& Above) :
<img src = "importance.png" height=200dp>

###### Creating Intent and Pending Intent in the Notification :
* Intent will be created to build the connectivity between the notification and the java class ,to navigate when clicked on notification.
```
Intent intent = Intent(this, MainActivity.class);
```
* Pending Intent will be created to connect the intent and the update type along with the notification id.
```
PendingIntent pendingIntent = PendingIntent.getActivity(this,NOTIFICATION_ID,intent,PendingIntent.FLAG_UPDATE_CURRENT);
```
### Updating a Notification :
* Update a notification by changing and or adding some of its content.
* Issue notification with updated parameters using builder.
* Call notify() passing in the same notification ID.
  * If previous notification is still visible, system updates.
  * If previous notification has been dismissed, new notification is delivered.

### Cancelling a Notification :
Notifications remain visible until:
* User dismisses it by swiping or by using "Clear All".
* Calling setAutoCancel() when creating the notification, removes it from the status bar when the user clicks on it.
* App calls cancel() or cancelAll() on NotificationManager.
```
manager.cancel(NOTIFICATION_ID);
```
