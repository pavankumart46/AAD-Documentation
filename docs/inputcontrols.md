## Input controls

This chapter introduces the Android _input controls_. Input controls are interactive elements in your app's UI that accept data input. Users input data to apps by entering text or numbers into fields using the on-screen keyboard. Users also select options from checkboxes, radio buttons, and drop-down menus, and they change settings and turn on or turn off certain features.

Android provides a variety of input controls for your UI. The figure below shows some popular ones.

![](https://github.com/saisankar12/document/blob/master/saisankar_concept_images/user_input_controls_composite.png?raw=true)

In the figure above:

1. [EditText](https://developer.android.com/reference/android/widget/EditText.html) field (subclass of TextView) for entering text using a keyboard
2. [SeekBar](https://developer.android.com/reference/android/widget/SeekBar.html) for sliding left or right to a setting
3. [CheckBox](https://developer.android.com/reference/android/widget/CheckBox.html) elements for selecting one or more options
4. [RadioGroup](https://developer.android.com/reference/android/widget/RadioGroup.html) of [RadioButton](https://developer.android.com/reference/android/widget/RadioButton.html) elements for selecting one option
5. [Switch](https://developer.android.com/reference/android/widget/Switch.html) for turning on or turning off an option
6. [Spinner](https://developer.android.com/reference/android/widget/Spinner.html) drop-down menu for selecting one option

When your app needs to get data from the user, try to make the process as easy for the user as it can be. For example, anticipate the source of the data, minimize the number of user gestures such as taps and swipes, and pre-fill forms when possible.

The user expects input controls to work in your app the same way they work in other apps. For example, users expect a _Spinner_ to show a drop-down menu, and they expect text-editing fields to show a keyboard when tapped. Don't violate established expectations, or you'll make it harder for your users to use your app.

### Input controls for making choices

Android offers ready-made input controls for the user to select one or more choices:

* [CheckBox](https://developer.android.com/reference/android/widget/CheckBox.html): Select one or more choices from a set of choices by tapping or clicking checkboxes.
* [RadioGroup](https://developer.android.com/reference/android/widget/RadioGroup.html) of radio buttons: Select one choice from a set of choices by clicking one circular "radio" button. Radio buttons are useful if you are providing only two or three choices.
* [ToggleButton](https://developer.android.com/reference/android/widget/ToggleButton.html) and [Switch](https://developer.android.com/reference/android/widget/Switch.html): Turn an option on or off.
* [Spinner](https://developer.android.com/reference/android/widget/Spinner.html): Select one choice from a set of choices in a drop-down menu. A Spinner is useful for three or more choices, and takes up little room in your layout.

### Input controls and the View focus

If your app has several UI input elements, which element gets input from the user first? 
  * For example, if you have several _EditText_ elements for the user to enter text, which element (that is, which View) receives the text? The [View](https://developer.android.com/reference/android/view/View.html) that "has the focus" receives user input.

Focus indicates which _View_ is selected. The user can initiate focus by tapping on a _View_, for example a specific _EditText_ element. You can define a focus order that defines how focus moves from one element to another when the user taps the Return key, Tab key, or arrow keys. You can also control focus programmatically by calling _requestFocus()_ on any _View_ that is focusable.

In addition to being focusable, input controls can be _clickable_. If a view's clickable attribute is set to _true_, then the view can react to click events. You can also make an element clickable programmatically.

What's the difference between focusable and clickable?

  * A _focusable_ view is allowed to gain focus from a touchscreen, external keyboard, or other input device.
  * A _clickable_ view is any view that reacts to being tapped or clicked.
  
Android-powered devices use many input methods, including directional pads (D-pads), trackballs, touchscreens, external keyboards, and more. Some devices, like tablets and smartphones, are navigated primarily by touch. Other device have no touchscreen. Because a user might navigate through your UI with an input device such as D-pad or a trackball, make sure you do the following:

* Make it visually clear which View has focus, so that the user knows where the input goes.
* Explicitly set the focus in your code to provide a path for users to navigate through the input elements using directional keys or a trackball.

Fortunately, in most cases you don't need to control focus yourself. Android provides "touch mode" for devices that respond to touch, such as smartphones and tablets. When the user begins interacting with the UI by touching it, only View elements with _isFocusableInTouchMode()_ set to _true_, such as text input fields, are focusable. Other _View_ elements that are touchable, such as _Button_ elements, don't take focus when touched. If the user clicks a directional key or scrolls with a trackball, the device exits "touch mode" and finds a view to take focus.

Focus movement is based on a natural algorithm that finds the nearest neighbor in a given direction:

* When the user taps the screen, the topmost View under the tap is in focus, providing touch access for the child View elements of the topmost View.
* If you set an EditText view to a single line (such as the textPersonName value for the [android:inputType](https://developer.android.com/reference/android/widget/TextView.html#attr_android:inputType) attribute), the user can tap the right-arrow key on the on-screen keyboard to close the keyboard and shift focus to the next input control View based on what the Android system finds.

  The system usually finds the nearest input control in the same direction the user was navigating (up, down, left, or right).

  If there are multiple input controls that are nearby and in the same direction, the system scans from left to right, top to bottom.

* Focus can also shift to a different View if the user interacts with a directional control, such as a D-pad or trackball.

You can influence the way Android handles focus by arranging input controls such as _EditText_ elements in a certain layout from left to right and top to bottom, so that focus shifts from one to the other in the sequence you want.

If the algorithm does not give you what you want, you can override it by adding the _nextFocusDown, nextFocusLeft, nextFocusRight,_ and _nextFocusUp_ XML attributes to your layout file:

1. Add one of these attributes to a View to decide where to go upon leaving the View—in other words, which View should be the next View.
2. Define the value of the attribute to be the id of the next View. For example:

```xml
<LinearLayout
    <!-- Other attributes... --> 
    android:orientation="vertical" >

    <Button android:id="@+id/top"
          <!-- Other Button attributes... --> 
          android:nextFocusUp="@+id/bottom" />

    <Button android:id="@+id/bottom"
          <!-- Other Button attributes... -->
          android:nextFocusDown="@+id/top"/>

</LinearLayout>
```

In a vertical _LinearLayout_, navigating up from the first _Button_ would not ordinarily go anywhere, nor would navigating down from the second _Button_. But in the example above, the 
_top_ Button has specified the bottom Button as the nextFocusUp (and vice versa), so the navigation focus will cycle from top-to-bottom and bottom-to-top.

To declare a View as focusable in your UI (when it is traditionally not), add the _android:focusable_ XML attribute to the View in the layout, and set its value to true. You can also declare a View as focusable while in "touch mode" by setting android:focusableInTouchMode set to true.

You can also explicitly set the focus or find out which View has focus by using the following methods:

* Call [onFocusChanged](https://developer.android.com/reference/android/view/View.html#onFocusChanged(boolean,%20int,%20android.graphics.Rect)) to determine where focus came from.
* To find out which View currently has the focus, call [Activity.getCurrentFocus()](https://developer.android.com/reference/android/app/Activity.html#getCurrentFocus()), or use [ViewGroup.getFocusedChild()](https://developer.android.com/reference/android/view/ViewGroup.html#getFocusedChild()) to return the focused child of a _View_ (if any).
* To find the _View_ in the hierarchy that currently has focus, use [findFocus()](https://developer.android.com/reference/android/view/ViewGroup.html#findFocus()).
* Use [requestFocus](https://developer.android.com/reference/android/view/View.html#requestFocus()) to give focus to a specific View.
* To change whether a View can take focus, call [setFocusable](https://developer.android.com/reference/android/view/View.html#setFocusable(boolean)).
* To set a listener that is notified when the View gains or loses focus, use [setOnFocusChangeListener](https://developer.android.com/reference/android/view/View.html#setOnFocusChangeListener(android.view.View.OnFocusChangeListener)).

you learn more about focus with EditText elements.

### Checkboxes

Use a set of checkboxes when you want the user to select any number of choices, including zero choices:

* Each checkbox is independent of the other boxes in the set, so selecting one box doesn't clear the other boxes. (If you want to limit the user's selection to one choice, use radio buttons.)
* A user can clear a checkbox that was already selected.

Users expect checkboxes to appear in a vertical list, like a to-do list, or side-by-side if the labels are short.

[Click For the Image](https://github.com/saisankar12/document/blob/master/saisankar_concept_images/checkboxes.png)

Each checkbox is a separate [CheckBox](https://developer.android.com/reference/android/widget/CheckBox.html) element in your XML layout. To create multiple checkboxes in a vertical orientation, use a vertical LinearLayout:

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
        android:orientation="vertical"
        android:layout_width="fill_parent"
        android:layout_height="fill_parent">

        <CheckBox android:id="@+id/checkbox1_chocolate"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="ChocolateSyrup" />
        <CheckBox android:id="@+id/checkbox2_sprinkles"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Sprinkles" />
        <CheckBox android:id="@+id/checkbox3_nuts"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="CrushedNuts" />

</LinearLayout>
```

Typically programs retrieve the state of each _CheckBox_ when a user taps or clicks a **Submit** or **Done** _Button_ in the same _Activity_, which uses the _android:onClick_ attribute to call a method such as _onSubmit()_:

```xml
<Button
   android:layout_width="wrap_content"
   android:layout_height="wrap_content"
   android:text="@string/submit"
   android:onClick="onSubmit"/>
```

The callback method—_onSubmit()_ in the example above—must be _public_, return _void_, and define a _View_ as a parameter (the view that was clicked). In this callback method you can determine whether a _CheckBox_ is selected by using the [isChecked()](https://developer.android.com/reference/android/widget/CompoundButton.html#isChecked()) method (inherited from [CompoundButton](https://developer.android.com/reference/android/widget/CompoundButton.html)).

The _isChecked()_ method returns _true_ if there is a check mark in the box. For example, the following statement assigns _true_ or _false_ to _checked_, depending on whether the checkbox is checked:

```java
public void onSubmit(View view) {
        CheckBox ch_java = findViewById(R.id.java);
        CheckBox ch_android = findViewById(R.id.android);
        StringBuilder builder = new StringBuilder();
        if(ch_java.isChecked()){
            builder.append(ch_java.getText().toString()+",");
        }

        if(ch_android.isChecked()){
            builder.append(ch_android.getText().toString());
        }
// Code to display the result...
}
```

**Tip**: To respond quickly to a _CheckBox_—such as display a message (like an alert), or show a set of further options—you can use the _android:onClick_ attribute in the XML layout for each _CheckBox_ to declare the callback method for that _CheckBox_. The callback method must be defined within the _Activity_ that hosts this layout.

For more information about checkboxes, see [Checkboxes](https://developer.android.com/guide/topics/ui/controls/checkbox.html) in the Android developer documentation.

### Radio buttons

Use radio buttons when you have two or more options that are mutually exclusive. When the user selects one, the others are automatically deselected. (If you want to enable more than one selection from the set, use checkboxes.)

![](https://github.com/saisankar12/document/blob/master/saisankar_concept_images/radiobuttons.png?raw=true)

Users expect radio buttons to appear as a vertical list, or side-by-side if the labels are short.

Each radio button is an instance of the [RadioButton](https://developer.android.com/reference/android/widget/RadioButton.html) class. Radio buttons are normally placed within a [RadioGroup](https://developer.android.com/reference/android/widget/RadioGroup.html) in a layout. When several RadioButton elements are inside a RadioGroup, selecting one RadioButton clears all the others.


Add RadioButton elements to your XML layout within a RadioGroup:

```xml
<RadioGroup
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:orientation="vertical"
        >
        <RadioButton
            android:id="@+id/sameday"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:onClick="onRadioButtonClicked"
            android:text="One" />
        <RadioButton
            android:id="@+id/nextday"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:onClick="onRadioButtonClicked"
            android:text="Two" />
        <RadioButton
            android:id="@+id/pickup"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:onClick="onRadioButtonClicked"
            android:text="Three" />
</RadioGroup>
```

Use the _android:onClick_ attribute for each _RadioButton_ to declare the click handler, which must be defined within the _Activity_ that hosts the layout. In the layout above, clicking any _RadioButton_ calls the same _onRadioButtonClicked()_ method in the _Activity_. You could also create separate click handlers in the _Activity_ for each _RadioButton_.

The click handler method must be _public_, return _void_, and define a _View_ as its only parameter (the view that was clicked). The following shows one click handler, _onRadioButtonClicked()_, for all the _RadioButton_ elements in the _RadioGroup_. It uses a _switch_ case block to check the resource _id_ for the _RadioButton_ element to determine which one was checked:

```java
public void onRadioButtonClicked(View view) {
   // Check to see if a button has been clicked.
   boolean checked = ((RadioButton) view).isChecked();
   // Check which radio button was clicked.
   switch(view.getId()) {
      case R.id.sameday:
         if (checked)
            // Code for same day service ...
            break;
      case R.id.nextday:
         if (checked)
            // Code for next day delivery ...
            break;
      case R.id.pickup:
         if (checked)
            // Code for pick up ...
            break;
   }
}
```

**Tip**: To give users a chance to review their radio button selection before the app responds, you could implement a **Submit** or **Done** button as shown previously with checkboxes, and remove the _android:onClick_ attributes from the radio buttons. Then add the _onRadioButtonClicked()_ method to the android:onClick attribute for the **Submit** or **Done** button.

For more information about radio buttons, see [Radio Buttons](https://developer.android.com/guide/topics/ui/controls/radiobutton.html) in the Android developer documentation.

### Spinner

A [Spinner](https://developer.android.com/reference/android/widget/Spinner.html) provides a quick way for the user to select one value from a set. The user taps on the spinner to see a drop-down list with all available values.

A spinner works well when the user has more than three choices, because spinners scroll as needed, and a spinner doesn't take up much space in your layout. If you are providing only two or three choices and you have space in your layout, you might want to use radio buttons instead of a spinner.

**Tip**: For more information about spinners, see the [Spinners](https://developer.android.com/guide/topics/ui/controls/spinner.html) guide.

![](https://github.com/saisankar12/document/blob/master/saisankar_concept_images/spinner-android.png?raw=true)

If you have a long list of choices, a spinner might extend beyond your layout, forcing the user to scroll. A spinner scrolls automatically, with no extra code needed. However, making the user scroll through a long list (such as a list of countries) isn't recommended, because it can be hard for the user to select an item.

To create a spinner, use the [Spinner](https://developer.android.com/reference/android/widget/Spinner.html) class, which creates a View that displays individual spinner values as child View elements and lets the user pick one. Follow these steps:

1. Create a Spinner element in your XML layout, and specify its values using an array and an [ArrayAdapter](https://developer.android.com/reference/android/widget/ArrayAdapter.html).
2. Create the _Spinner_ and its adapter using the [SpinnerAdapter](https://developer.android.com/reference/android/widget/SpinnerAdapter.html) class.
3. To define the selection callback for the Spinner, update the _Activity_ that uses the _Spinner_ to implement the [AdapterView.OnItemSelectedListener](https://developer.android.com/reference/android/widget/AdapterView.OnItemSelectedListener.html) interface.

### Create the Spinner UI element

To create a spinner in your XML layout, add a Spinner element, which provides the drop-down list:

```xml
<Spinner
   android:id="@+id/label_spinner"
   android:layout_width="wrap_content"
   android:layout_height="wrap_content"/>
```

### Specify values for the Spinner

Add an adapter that fills the _Spinner_ list with values. An adapter is like a bridge, or intermediary, between two incompatible interfaces. For example, a memory card reader acts as an adapter between the memory card and a laptop. You plug the memory card into the card reader, and plug the card reader into the laptop, so that the laptop can read the memory card.

The adapter takes the data set you've specified (an array in this example), and makes a _View_ for each item in the data set (a _View_ within the _Spinner_), as shown in the figure below.

![](https://github.com/saisankar12/document/blob/master/saisankar_concept_images/dg_adapter_view.png?raw=true)

The [SpinnerAdapter](https://developer.android.com/reference/android/widget/SpinnerAdapter.html) class, which implements the _Adapter_ class, allows you to define two different views: one that shows the data values in the _Spinner_ itself, and one that shows the data in the drop-down list when the _Spinner_ is touched or clicked.

The values you provide for the _Spinner_ can come from any source, but must be provided through a 
_SpinnerAdapter_, such as an [ArrayAdapter](https://developer.android.com/reference/android/widget/ArrayAdapter.html) if the values are easily stored in an array. The following shows a simple array called _labels_array_ of predetermined values in the **_strings.xml_** file:

```xml
<string-array name="labels_array">
        <item>Home</item>
        <item>Work</item>
        <item>Mobile</item>
        <item>Other</item>
</string-array>
```

**Tip**: You can use a CursorAdapter if the values are provided from a source such as a stored file or a database. You learn more about stored data in another lesson.

### Create the Spinner and its adapter

Create the _Spinner_, and set its listener to the _Activity_ that implements the callback methods. The best place to do this is after the _Activity_ layout is inflated in the _onCreate()_ method. Follow these steps:

1. Instantiate a _Spinner_ in the _onCreate()_ method using the _label_spinner_ element in the layout, and set its listener _(spinner.setOnItemSelectedListener)_ in the _onCreate()_ method, as shown in the following code snippet:

```java
@Override
 protected void onCreate(Bundle savedInstanceState) {
    // ... Rest of onCreate code ...
    // Create the spinner.
    Spinner spinner = findViewById(R.id.label_spinner);
    if (spinner != null) {
             spinner.setOnItemSelectedListener(this);
    }
    // Create ArrayAdapter using the string array and default spinner layout.
```

The code snippet above uses findViewById() to find the Spinner by its id (label_spinner). It then sets the _onItemSelectedListener_ to whichever Activity implements the callbacks (this) using the [setOnItemSelectedListener()](https://developer.android.com/reference/android/widget/AdapterView.html#setOnItemSelectedListener(android.widget.AdapterView.OnItemSelectedListener)) method


2. Continuing to edit the onCreate() method, add a statement that creates the ArrayAdapter with the string array (labels_array) using the Android-supplied Spinner layout for each item (layout.simple_spinner_item):

```java
 String[] branch = getResources().getStringArray(R.array.branches);
 ArrayAdapter<String> arrayAdapter=new ArrayAdapter<>(this,android.R.layout.simple_list_item_1,branch);
```

3. Specify the layout for the Spinner choices to be simple_spinner_dropdown_item, and then apply the adapter to the Spinner:

```java
spinner.setAdapter(arrayAdapter);
```

The snippet above uses [setAdapter()](https://developer.android.com/reference/android/widget/AdapterView.html#setAdapter(T)) to apply the adapter to the Spinner. You should use the simple_spinner_dropdown_item default layout, unless you want to define your own layout for the Spinner appearance.

### Add code to respond to Spinner selections

When the user chooses an item from the spinner's drop-down list, here's what happens and how you retrieve the item:

1. The Spinner receives an on-item-selected event.
2. The event triggers the calling of the onItemSelected() callback method of the [AdapterView.OnItemSelectedListener](https://developer.android.com/reference/android/widget/AdapterView.OnItemSelectedListener.html) interface.
3. Retrieve the selected item in the Spinner using the [getItemAtPosition()](https://developer.android.com/reference/android/widget/AdapterView.html#getItemAtPosition(int)) method of the _AdapterView_ class:

```java
spinner.setOnItemSelectedListener(new AdapterView.OnItemSelectedListener() {
        @Override
        public void onItemSelected(AdapterView<?> parent, View view, int position, long id) {
           //Implement Your Action
        }
        @Override
        public void onNothingSelected(AdapterView<?> parent) {
            //Implement Your Action
        }
});
```

The arguments for onItemSelected() are as follows:

| parent AdapterView  | The AdapterView where the selection happened |
| ------------- | ------------- |
| view View  | The View within the AdapterView that was clicked  |
| int pos  | The position of the View in the adapter  |
| long id | The row id of the item that is selected  |

Implement/override the _onNothingSelected()_ callback method of the [AdapterView.OnItemSelectedListener](https://developer.android.com/reference/android/widget/AdapterView.OnItemSelectedListener.html) interface to do something if nothing is selected.

For more information about using spinners, see [Spinners](https://developer.android.com/guide/topics/ui/controls/spinner.html) in the Android developer documentation.

### Practical Example:

**activity_mail.xml**

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="10dp"
    tools:context=".UserInoutControls">

    <ImageView
        android:layout_width="100dp"
        android:layout_height="100dp"
        android:layout_gravity="center"
        android:src="@mipmap/ic_launcher" />

    <EditText
        android:id="@+id/name"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter your name"
        android:layout_marginTop="10dp"
        android:inputType="textCapWords" />

    <EditText
        android:id="@+id/email"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter your emailid"
        android:inputType="textEmailAddress"
        android:layout_marginTop="10dp"/>

    <EditText
        android:id="@+id/mobile"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter your mobileno"
        android:inputType="number"
        android:layout_marginTop="10dp"/>

    <EditText
        android:id="@+id/password"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter your password"
        android:inputType="textPassword"
        android:layout_marginTop="10dp"/>

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Gender"
        android:layout_marginTop="10dp"
        android:textSize="20sp" />

    <RadioGroup
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:layout_marginTop="10dp">

        <RadioButton
            android:id="@+id/malerb"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Male" />

        <RadioButton
            android:id="@+id/femalerb"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Female" />
    </RadioGroup>

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Technical Skills"
        android:layout_marginTop="10dp"
        android:textSize="20sp" />

    <CheckBox
        android:id="@+id/java"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Java"
        android:layout_marginTop="10dp"/>

    <CheckBox
        android:id="@+id/android"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Android"
        android:layout_marginTop="10dp"/>

    <Spinner
        android:id="@+id/branchsp"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:entries="@array/branches" />

    <Button
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:onClick="displyData"
        android:text="Display" />

    <ScrollView
        android:layout_width="match_parent"
        android:layout_height="match_parent">

        <TextView
            android:id="@+id/result"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="ResultData"
            android:textSize="30sp" />
    </ScrollView>
</LinearLayout>
```

### string.xml

```xml
<string-array name="branches">
        <item></item>
        <item>CSE</item>
        <item>ECE</item>
        <item>EEE</item>
        <item>IT</item>
        <item>Mech</item>
</string-array>
```

### MainActivity.java

```java
import android.os.Bundle;
import android.view.View;
import android.widget.CheckBox;
import android.widget.EditText;
import android.widget.RadioButton;
import android.widget.Spinner;
import android.widget.TextView;

import androidx.appcompat.app.AppCompatActivity;

public class UserInoutControls extends AppCompatActivity {

    EditText et_name, et_email, et_phone, et_pass;
    RadioButton r_male, r_female;
    CheckBox ch_java, ch_android;
    Spinner sp_branch;
    TextView tv_data;
    String gender;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        et_name = findViewById(R.id.name);
        et_email = findViewById(R.id.email);
        et_phone = findViewById(R.id.mobile);
        et_pass = findViewById(R.id.password);

        tv_data = findViewById(R.id.result);

        r_male = findViewById(R.id.malerb);
        r_female = findViewById(R.id.femalerb);

        ch_java = findViewById(R.id.java);
        ch_android = findViewById(R.id.android);

        sp_branch = findViewById(R.id.branchsp);

    }

    public void displyData(View view) {
        String name = et_name.getText().toString();
        String email = et_email.getText().toString();
        String phone = et_phone.getText().toString();
        String pass = et_pass.getText().toString();
        if (r_male.isChecked()) {
            gender = r_male.getText().toString();
        } else if (r_female.isChecked()) {
            gender = r_female.getText().toString();
        }
        StringBuilder builder = new StringBuilder();
        if (ch_java.isChecked()) {
            builder.append(ch_java.getText().toString() + ",");
        }

        if (ch_android.isChecked()) {
            builder.append(ch_android.getText().toString());
        }

        String branch = sp_branch.getSelectedItem().toString();


        tv_data.setText(name + "\n" + email + "\n" + phone + "\n" + pass + "\n" +
                gender + "\n" + builder.toString() + "\n" + branch);

    }
}
```

### Output
![](https://github.com/saisankar12/document/blob/master/saisankar_concept_images/userinputcontrol_output.jpg?raw=true)
