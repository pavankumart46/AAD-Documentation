# Shared preferences

Shared preferences allow you to store small amounts of primitive data as key/value pairs in a file on the device. To get a handle to a preference file, and to read, write, and manage preference data, use the SharedPreferences class. The Android framework manages the shared preferences file itself. The file is accessible to all the components of your app, but it is not accessible to other apps.

For managing large amounts of data, use an SQLite database or other suitable storage option

### Shared preferences vs. saved instance state

Shared preferences | Saved instance state
------------------ | --------------------
Persists across user sessions, even if your app is stopped and restarted, or if the device is rebooted.| Preserves state data across activity instances in the same user session.
Used for data that should be remembered across user sessions, such as a user's preferred settings or their game score.| Used for data that should not be remembered across sessions, such as the currently selected tab, or any current state of an activity.
Represented by a small number of key/value pairs. | Represented by a small number of key/value pairs.
Data is private to the app. | Data is private to the app.
Common use is to store user preferences. | Common use is to recreate state after the device has been rotated.

### Writing the data into Shared Preference

If you want to work with shared prefrences first we should have to create the object for **SharedPrefrence** class.

There are Two ways to get the **SharedPrefrence** class Object:
```java
//It is used to store the multiple Activitys data into a Shared Prefrence
SharedPrefrence mPreferences = getSharedPreferences(sharedPrefFile, MODE_PRIVATE);
(OR)
//It is used to store single Activity Data into a Shared Prefrence
SharedPrefrence mPreferences = getPreference(MODE_PRIVATE);
```
### Code lab for SharedPrefrence
1. First create a one new AndroidStudio project(Select the Empty Activity) with the name of **SharedPreferenceTest**
### XML Code
```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".MainActivity">

   <EditText
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:hint="Enter username"
       android:id="@+id/username"
       />
    <EditText
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter password"
        android:id="@+id/password"
        android:inputType="textPassword"
        />
    <Button
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Login"
        android:onClick="login"
        />


</LinearLayout>
```
- Now I want to write the data into a shared prefrences, for that there is class called **SharedPrefrences.Editor**.
- lets create a object for **SharedPrefrences.Editor** class Object.
- After creating the **Sharedprences.Editor** class object, In this class so many methods are available suppose if you want to store the String value there is a method called
**putString()** same like that **putInt()**,**putFloat()**,**putBoolean()** etc....
- In the last we should commit the values for that we can use two methods 
      - editor.apply()
      - editor.commit()

```java
 @Override
    protected void onPause() {
        super.onPause();
        SharedPreferences.Editor editor = mPreferences.edit();
        editor.putString("uname",et_u.getText().toString());
        editor.putString("pass",et_p.getText().toString());
        editor.apply();
    }
```
- In the oncreate method we can retrive the values and set it to the respective Edittext's.
- If you want to retrive the data from the shared prefrences, through the **SharedPrefrences** class object we can access it.


               - If you want to access the string values there is a method called getString()
               - If you want to access the int values there is a method called getInt()
```java
 EditText et_u,et_p;
 SharedPreferences preferences;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        et_u = findViewById(R.id.username);
        et_p = findViewById(R.id.password);
        preferences = getSharedPreferences("MASTAN",MODE_PRIVATE);
        if(preferences!=null){
            String name=preferences.getString("uname","Data not found");
            String pass=preferences.getString("pass","Data not found");
            et_u.setText(name);
            et_p.setText(pass);
        }else{
            Toast.makeText(this,
                    "In Prefrence there is no data", Toast.LENGTH_SHORT).show();
        }
    }

```
