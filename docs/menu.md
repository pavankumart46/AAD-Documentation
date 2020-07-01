# Menus
## Types of Menus

A menu is a set of options. The user can select from a menu to perform a function, for example searching for information, saving information, editing information, or navigating to a screen. The figure below shows the types of menus that the Android system offers. 

<br>
<p align="center">
<img  src="https://github.com/saisankar12/document/blob/master/saisankar_concept_images/types_menus.png">
</p>

1. **App bar with Options menu:** Appears in the app bar and provides the primary options that affect use of the app itself.
    - Examples of menu options: 
      - Search to perform a search
      - Share to share a link
      - Settings** to navigate to a Settings *Activity*.
2. **Contextual menu:** Appears as a floating list of choices when the user performs a long tap on an element on the screen. 
    - Examples of menu options: 
      - Edit to edit the element
      - Delete to delete it
      - Share to share it over social media.
3. **Contextual action bar:** Appears at the top of the screen overlaying the app bar, with action items that affect the selected element or elements. 
    - Examples of menu options: 
        - Edit, Share, and Delete for one or more selected elements.
4. **Popup menu:** Appears anchored to a View such as an ImageButton, and provides an overflow of actions or the second part of a two-part command. 
    - Example of a popup menu: 
      - the Gmail app anchors a popup menu to the app bar for the message view with Reply, Reply All, and Forward.

## App bar with options menu

The app bar (also called the action bar) is a dedicated space at the top of each **_Activity_** screen. When you create an **_Activity_** from a template (such as Empty Template), an app bar is automatically included for the **_Activity_**.

The app bar by default shows the app title, or the name defined in **_AndroidManifest.xml_** by the **_android:label_** attribute for the **_Activity_**. The app bar may also include the Up button for navigating up to the parent activity. Up navigation is described in the chapter on using the app bar for navigation.

The options menu in the app bar usually provides navigation to other screens in the app, or options that affect using the app itself. (The options menu should not include options that act on an element on the screen. For that you use a contextual menu, described later in this chapter.)

For example, your options menu might let the user navigate to another activity to place an order. Or your options menu might let the user change settings or profile information, or do other actions that have a global impact on the app.

The options menu appears in the right corner of the app bar. The app bar is split into four functional areas that apply to most apps, as shown in the figure below.

<br>
<p align="center">
<img  src="https://github.com/saisankar12/document/blob/master/saisankar_concept_images/option%20_menu.png">
</p>
<br>

In the figure above:

1. **_Navigation button or Up button:_** Use a navigation button in this space to open a navigation drawer, or use an Up button for navigating up through your app's screen hierarchy to the parent activity. Both are described in the next chapter.
2. **_Title:_** The title in the app bar is the app title, or the name defined in **_AndroidManifest.xml_** by the **android:label** attribute for the activity.
3. **_Action icons for the options menu:_** Each action icon appears in the app bar and represents one of the options menu's most frequently used items. Less frequently used options menu items appear in the overflow options menu.
4. **_Overflow options menu:_** The overflow icon opens a popup with option menu items that are not shown as icons in the app bar.


## Adding the options menu

Android provides a standard XML format to define options menu items. Instead of building the menu in your **_Activity_** code, you can define the menu and all its items in an XML [menu resource](https://developer.android.com/guide/topics/resources/menu-resource.html). A menu resource defines an application menu (options menu, context menu, or popup menu) that can be inflated with [MenuInflater](https://developer.android.com/reference/android/view/MenuInflater.html), which loads the resource as a [Menu](https://developer.android.com/reference/android/view/Menu.html) object in your Activity.

If you start an app project using the Basic Activity template, the template adds the menu resource for you and inflates the options menu with **_MenuInflater_**, so you can skip this step and go right to "Defining how menu items appear".

If you are not using the Basic Activity template, use the resource-inflate design pattern, which makes it easy to create an options menu. Follow these steps (refer to the figure below):

<br>
<p align="center">
<img  src="https://github.com/saisankar12/document/blob/master/saisankar_concept_images/dg_options_menu_design_pattern.png">
</p>
<br>

   1. **XML menu resource.** Create an XML menu resource file for the menu items, and assign appearance and position attributes as described in the next section.
   2. **Inflating the menu.** Override the [onCreateOptionsMenu()](https://developer.android.com/reference/android/app/Activity.html#onCreateOptionsMenu(android.view.Menu)) method in your **_Activity_** to inflate the menu.
   3. **Handling menu-item clicks.** Menu items are View elements, so you can use the **_android:onClick_** attribute for each menu item. However, the [onOptionsItemSelected()](https://developer.android.com/reference/android/app/Activity.html#onOptionsItemSelected(android.view.MenuItem)) method can handle all the menu-item clicks in one place and determine which menu item the user clicked, which makes your code easier to understand.
   4. **Performing actions.** Create a method to perform an action for each options menu item.


## Steps To Create App bar with options menu

   1. Create AndroidResourse directory
        * Select the **res** folder in the **Project > Android** pane and choose **File > New > Android resource directory.**
        <br>
        <p align="center">
            <img  src="https://github.com/saisankar12/document/blob/master/saisankar_concept_images/dircectory_creation.PNG">
        </p>
        <br>
        
        * Choose **menu** in the **Resource** type drop-down menu, and click **OK.**
        <br>
        <p align="center">
            <img  src="https://github.com/saisankar12/document/blob/master/saisankar_concept_images/menu_resourse_directory.PNG">
        </p>
        <br>
        
   2. XML menu resource (filename.xml)
       * Select the new **menu** folder, and choose **File > New > Menu resource file.**
        <br>
        <p align="center">
            <img  src="https://github.com/saisankar12/document/blob/master/saisankar_concept_images/menuxml_file_creation.PNG">
        </p>
        <br>
        
        * Enter the name, such as **Ex: menu_main**, and click **OK**. The new **_menu_main.xml_** file now resides within the **menu** folder.
        <br>
        <p align="center">
            <img  src="https://github.com/saisankar12/document/blob/master/saisankar_concept_images/menu_xml_file.PNG">
        </p>
        <br>
        
        * Add menu items using the **_<item ... />_** tag. <br>
        
```xml
<item
    android:id="@+id/user"
    android:title="User"/>
```
<br>

* Adding icons for menu items
       
 <br>
        <p align="center">
            <img  src="https://github.com/saisankar12/document/blob/master/saisankar_concept_images/image_creation.PNG">
        </p>
 <br>
        
* Icon and appearance attributes            
            - Use the following attributes to govern the menu item's appearance:
                  _android:icon:_ An image to use as the menu item icon. For example, the following menu item defines ic_order_white as its icon:
                  
```xml
<item
    android:id="@+id/user"
    android:title="User"
    android:icon="@mipmap/user"
        />
```
   <br>  
       
* Use the **_app:showAsAction_** attribute to show menu items as icons in the app bar, with the following values:

     - **_"always":_** Always place this item in the app bar. Use this only if it's critical that the item appear in the app bar (such as a Search icon). If you set   multiple items to always appear in the app bar, they might overlap something else in the app bar, such as the app title.
     - **_"ifRoom":_** Only place this item in the app bar if there is room for it. If there is not enough room for all the items marked **_"ifRoom"_**, the items with the lowest **_orderInCategory_** values are displayed in the app bar. The remaining items are displayed in the overflow menu.
     - **_"never":_** Never place this item in the app bar. Instead, list the item in the app bar's overflow menu.
     - **_"withText":_** Also include the title text (defined by **_android:title_**) with the item. This attribute is used primarily to include the title with the icon in the app bar, because if the item appears in the overflow menu, the title text appears regardless.
       
### Position attributes
       
* Use the **_android:orderInCategory_** attribute to specify the order in which the menu items appear in the menu, with the lowest number appearing higher in the menu. This is usually the order of importance of the item within the menu. For example, if you want **Order** to be first, followed by **Status, Favorites,** and **Contact**, the following table shows the priority of these items in the menu:
       <br>
           
    Menu item | orderInCategory attribute
    ----------|----------------------------
    Order | 10 
    Status | 20
    Favorites | 30 
    Contact | 40 
       
<br>
        <p align="center">
            <img  src="https://github.com/saisankar12/document/blob/master/saisankar_concept_images/orderattribute.PNG">
        </p>
 <br>
     
```xml 
     <item
        android:title="Call"
        android:id="@+id/call"
        android:icon="@mipmap/call"
        android:orderInCategory="40"
        app:showAsAction="always"
        />
  ```
   3. onCreateOptionsMenu() to inflate the menu
        - If you start an app project using the Basic Activity template, the template adds the code for inflating the options menu with **_MenuInflater
_**, so you can skip this step.

        - If you are not using the Basic Activity template, inflate the menu resource in your activity by overriding the [onCreateOptionsMenu()](https://developer.android.com/reference/android/app/Activity.html#onCreateOptionsMenu(android.view.Menu)) method and using the [getMenuInflater()](https://developer.android.com/reference/android/app/Activity.html#getMenuInflater()) method of the **Activity** class.

        - The **getMenuInflater()** method returns a [MenuInflater](https://developer.android.com/reference/android/view/MenuInflater.html), which is a class used to instantiate menu XML files into **Menu** objects. The **MenuInflater** class provides the [inflate()](https://developer.android.com/reference/android/view/MenuInflater.html#inflate(int,%20android.view.Menu)) method, which takes two parameters:
            - The resource **_id_** for an XML layout resource to load (**_R.menu.menu_main_** in the following example).
            - The [Menu](https://developer.android.com/reference/android/view/Menu.html) to inflate into (_menu_ in the following example)
```java
     @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        getMenuInflater().inflate(R.menu.menu,menu);
        return super.onCreateOptionsMenu(menu);
    }
```
     
   4. onClick attribute or onOptionsItemSelected() 
        - However, the [onOptionsItemSelected()](https://developer.android.com/reference/android/app/Activity.html#onOptionsItemSelected(android.view.MenuItem)) method can handle all the menu-item clicks in one place and determine which menu item the user clicked. This makes your code easier to understand.
```java
     @Override
    public boolean onOptionsItemSelected(@NonNull MenuItem item) {
        //Action
        return super.onOptionsItemSelected(item);
    }
```
<br>

* For example, you can use a **_switch case_** block to call the appropriate method (such as **Toast** message) based on the menu item's **_id_.** You retrieve the **_id_** using the [getItemId()](https://developer.android.com/reference/android/widget/Adapter.html#getItemId(int)) method:
<br>

```java
     @Override
    public boolean onOptionsItemSelected(@NonNull MenuItem item) {
        switch (item.getItemId()){
            case R.id.notification:
                Toast.makeText(this, ""+item.getTitle(), Toast.LENGTH_SHORT).show();
                break;
            case R.id.dial:
                Toast.makeText(this, ""+item.getTitle(), Toast.LENGTH_SHORT).show();
                break;
            case R.id.call:
                Toast.makeText(this, ""+item.getTitle(), Toast.LENGTH_SHORT).show();
                break;
        }
        return super.onOptionsItemSelected(item);
    }
```
<br>
    
## Codeing Implementation
- Create Start new android Studio Project and Select Empty Activity
- No need modify your **_activity_main.xml_**, If any requriments you can modify it.
- Create Android Resourse Directory with the name of menu 
- Create menu resourse xml file
- adding items
- intialization in java file 
- handling the click events
    
### activity_main.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".MainActivity">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello World!"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />
    
</androidx.constraintlayout.widget.ConstraintLayout>


```
 ### menu.xml
 ```xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto">

    <item
        android:id="@+id/notification"
        android:title="Search" />
    <item
        android:id="@+id/dial"
        android:title="Dail" />
    <item
        android:id="@+id/call"
        android:icon="@mipmap/call"
        android:title="Call"
        app:showAsAction="always" />
    <item
        android:id="@+id/user"
        android:title="User" />
    
</menu>
    
 ```
    
### MainActivity.java
```java
package com.example.menuspickers;


import android.os.Bundle;
import android.view.Menu;
import android.view.MenuItem;
import android.widget.Toast;
import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }

    @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        getMenuInflater().inflate(R.menu.menu, menu);
        return super.onCreateOptionsMenu(menu);
    }

    @Override
    public boolean onOptionsItemSelected(@NonNull MenuItem item) {

        switch (item.getItemId()) {
            case R.id.notification:
                // we are getting menu item title here
                Toast.makeText(this, ""+item.getTitle(), Toast.LENGTH_SHORT).show();
                break;
            case R.id.dial:
                Toast.makeText(this, ""+item.getTitle(), Toast.LENGTH_SHORT).show();
                break;
            case R.id.call:
                Toast.makeText(this, ""+item.getTitle(), Toast.LENGTH_SHORT).show();
                break;
        }
        return super.onOptionsItemSelected(item);
    }

}
```
    
## Contextual Menus
    
Use a contextual menu to allow users to take an action on a selected [View](https://developer.android.com/reference/android/view/View.html). Contextual menus are most often used for items in a [ListView](https://developer.android.com/reference/android/widget/ListView.html), [RecyclerView](https://developer.android.com/reference/android/support/v7/widget/RecyclerView.html), [GridView](https://developer.android.com/reference/android/widget/GridView.html), or other view collection in which the user can perform direct actions on each item.

* Android provides two kinds of contextual menus:

    * A **_context menu_**, shown on the left side in the figure below, appears as a floating list of menu items when the user performs a long tap on a _View_. It is typically used to modify the View or use it in some fashion. 
        - For example, a context menu might include 
            - **Edit** to edit the contents of a _View_, 
            - **Delete** to delete a _View_,
            - **Share** to share a _View_ over social media. Users can perform a contextual action on one selected View at a time.

    * A **_contextual action bar_**, shown on the right side of the figure below, appears at the top of the screen in place of the app bar or underneath the app bar, with action items that affect one or more selected _View_ elements. Users can perform an action on multiple _View_ elements at once, if your app allows it.
    
<br>
        <p align="center">
            <img  src="https://github.com/saisankar12/document/blob/master/saisankar_concept_images/Context%20Menu%20Types.jpg">
        </p>
 <br>

### Floating context menu

<p>
    The familiar resource-inflate design pattern is used to create a context menu, modified to include registering (associating) the context menu with a _View_. The pattern consists of the steps shown in the figure below.
<p>

<br>
        <p align="center">
            <img  src="https://github.com/saisankar12/document/blob/master/saisankar_concept_images/contextmenufloating.png">
        </p>
 <br>

#### Steps to Implement Context Menu:
     
1. Create an XML menu resource file for the menu items. Assign appearance and position attributes as described in the previous section for the options menu.
2. Register a View to the context menu using the [registerForContextMenu()](https://developer.android.com/reference/android/app/Activity.html#registerForContextMenu(android.view.View)) method of the _Activity_ class.
3. Implement the [onCreateContextMenu()](https://developer.android.com/reference/android/view/View.OnCreateContextMenuListener.html#onCreateContextMenu(android.view.ContextMenu,%20android.view.View,%20android.view.ContextMenu.ContextMenuInfo)) method in your _Activity_ to inflate the menu.
4. Implement the [onContextItemSelected()](https://developer.android.com/reference/android/app/Activity.html#onContextItemSelected(android.view.MenuItem)) method in your _Activity_ to handle menu-item clicks.
5. Create a method to perform an action for each context menu item.
     
     
#### Creating the XML resource file
     
To create the XML menu resource directory and file, follow the steps in the previous section for the options menu. However, use a different name for the file, such as menu_context. Add the context menu items within _<item ... />_ tags.
     
For example, the following code defines the **_Edit_** menu item:
     
```xml
<item
   android:id="@+id/context_edit"
   android:title="Edit"
   android:orderInCategory="10"/>
```
    
### Registering a View to the context menu
     
To register a View to the context menu, call the [registerForContextMenu()](https://developer.android.com/reference/android/app/Activity.html#registerForContextMenu(android.view.View)) method with the View. Registering a context menu for a view sets the [View.OnCreateContextMenuListener](https://developer.android.com/reference/android/view/View.OnCreateContextMenuListener.html) on the View to this activity, so that [onCreateContextMenu()](https://developer.android.com/reference/android/app/Activity.html#onCreateContextMenu(android.view.ContextMenu,%20android.view.View,%20android.view.ContextMenu.ContextMenuInfo)) is called when it's time to show the context menu. (You implement onCreateContextMenu in the next section.)
     
For example, in the _onCreate()_ method for the _Activity_, you would add _registerForContextMenu()_:
     
```java
// Registering the context menu to the TextView of the article.
ListView names_list = findViewById(R.id.list);

// Create String Array
String[] s ={"Anusha","Pavan","Krishna","Siva","Masthan","Muni","Sai","Gopal","Chaitanya","Vara Prasad",
                "Anusha","Pavan","Krishna","Siva","Masthan","Muni","Sai","Gopal","Chaitanya","Vara Prasad"};

// For Displaying String Array Data in ListView, For That we need Create ArrayAdapter Like Below
ArrayAdapter<String> adapter=new ArrayAdapter<>(this,android.R.layout.simple_list_item_1,s);
     
// set Adapter to ListView, Then Only we can display the data in ListView        
lv.setAdapter(adapter);
registerForContextMenu(names_list);
```
     
Multiple views can be registered to the same context menu. If you want each item in a [TextView](https://developer.android.com/reference/android/widget/TextView.html) or [ListView](https://developer.android.com/reference/android/widget/ListView.html) or [GridView](https://developer.android.com/reference/android/widget/GridView.html) to provide the same context menu, register all items for a context menu by passing the [TextView](https://developer.android.com/reference/android/widget/TextView.html) or [ListView](https://developer.android.com/reference/android/widget/ListView.html) or [GridView](https://developer.android.com/reference/android/widget/GridView.html) to [registerForContextMenu()](https://developer.android.com/reference/android/app/Activity.html#registerForContextMenu(android.view.View)).
     
### Implementing the _onCreateContextMenu()_ method
     
When the registered View receives a long-click event, the system calls the [onCreateContextMenu()](https://developer.android.com/reference/android/view/View.OnCreateContextMenuListener.html#onCreateContextMenu(android.view.ContextMenu,%20android.view.View,%20android.view.ContextMenu.ContextMenuInfo)) method, which you can override in your _Activity_. (Long-click events are also called touch & hold events and _long-press_ events.)
     
The _onCreateContextMenu()_ method is where you define the menu items, usually by inflating a menu resource.

For example:

```java
     @Override
    public void onCreateContextMenu(ContextMenu menu, View v, ContextMenu.ContextMenuInfo menuInfo) {
        MenuInflater inflater = getMenuInflater();
        inflater.inflate(R.menu.menu,menu);
        super.onCreateContextMenu(menu, v, menuInfo);
    }
```
     
In the code above:

   - The _menu_ parameter for _onCreateContextMenu()_ is the context menu to be built.
   - The _v_ parameter is the _View_ registered for the context menu.
   - The _menuInfo_ parameter is extra information about the _View_ registered for the context menu. This information varies depending on the class of the _v_ parameter, which could be a _RecyclerView_ or a _GridView_.

   If you are registering a _RecyclerView_ or a _GridView_, you instantiate a [ContextMenu.ContextMenuInfo](https://developer.android.com/reference/android/view/ContextMenu.ContextMenuInfo.html) object to provide information about the item selected, and pass it as menuInfo, such as the row id, position, or child _View_.
     
The [MenuInflater](https://developer.android.com/reference/android/view/MenuInflater.html) class provides the [inflate()](https://developer.android.com/reference/android/view/MenuInflater.html#inflate(int,%20android.view.Menu)) method, which takes two parameters:

   - The resource _id_ for an XML layout resource to load. In the example above, the _id_ is _menu_context_.
   - The [Menu](https://developer.android.com/reference/android/view/Menu.html) to inflate into. In the example above, the _Menu_ is _menu_.

### Implementing the onContextItemSelected() method
     
When the user clicks on a menu item, the system calls the [onContextItemSelected()](https://developer.android.com/reference/android/app/Activity.html#onContextItemSelected(android.view.MenuItem)) method. You override this method in your _Activity_ in order to determine which menu item was clicked, and for which view the menu is appearing. You also use it to implement the appropriate action for the menu items, such as _editNote()_ , _shareNote()_ and _deleteNote()_ in the following code snippet for the **_Edit_** , **_Share_** and **_Delete_** menu items:
    
```java
     @Override
    public boolean onContextItemSelected(@NonNull MenuItem item) {
        switch (item.getItemId()){
            case R.id.share:
                // You can Write your requirement code here
                Toast.makeText(this, item.getTitle(), Toast.LENGTH_SHORT).show();
                break;
            case R.id.edit:
                // You can Write your requirement code here
                Toast.makeText(this, item.getTitle(), Toast.LENGTH_SHORT).show();
                break;
            case R.id.delete:
                // You can Write your requirement code here
                Toast.makeText(this, item.getTitle(), Toast.LENGTH_SHORT).show();
                break;
        }
        return super.onContextItemSelected(item);
    }
```
   
The above code snippet uses the [getItemId()](https://developer.android.com/reference/android/view/MenuItem.html#getItemId()) method to get the _id_ for the selected menu item, and uses it in a _switch case_ block to determine which action to take. The _id_ is the _android:id_ attribute assigned to the menu item in the XML menu resource file.

When the user performs a long-click on the article in the _ListView_, the floating context menu appears and the user can click a menu item.
     
<br>
        <p align="center">
            <img  src="https://github.com/saisankar12/document/blob/master/saisankar_concept_images/ContextMenuExample.jpg">
        </p>
 <br>
     
If you are using the _menuInfo_ information for a _RecyclerView_ or a _GridView_, you would add a statement before the _switch case_ block to gather the specific information about the selected _View_ (for _info_) by using [AdapterView.AdapterContextMenuInfo](https://developer.android.com/reference/android/widget/AdapterView.AdapterContextMenuInfo.html):
     
```java
     AdapterView.AdapterContextMenuInfo info = (AdapterView.AdapterContextMenuInfo) item.getMenuInfo();
```
     
## Contextual action bar Menu
     
A **_contextual action bar_** appears at the top of the screen to present actions the user can perform on a _View_ after long-clicking the _View_, as shown in the figure below.
     
     
<br>
        <p align="center">
            <img  src="https://github.com/saisankar12/document/blob/master/saisankar_concept_images/context_actionbar_singlecomponent.jpg">
        </p>
 <br>
     
In the above figure:

1. **Contextual action bar**. The bar offers three actions on the right side (**Edit**, **Share**, and **Delete**) and the Done button (left arrow icon) on the left side.
2. **View**. View on which a long-click triggers the contextual action bar.
     
The contextual action bar appears only when contextual action mode, a system implementation of [ActionMode](https://developer.android.com/reference/android/view/ActionMode.html), occurs as a result of the user performing a long-click on one or more selected _View_ elements.

_ActionMode_ represents UI mode for providing alternative interaction, replacing parts of the normal UI until finished. 
    - For example, text selection is implemented as an _ActionMode_, as are contextual actions that work on a selected item on the screen. Selecting a section of text or long-clicking a view triggers _ActionMode_.

While this mode is enabled, the user can select multiple items, if your app allows it. The user can also deselect items, and continue to navigate within the activity. _ActionMode_ is disabled when one of the following things occur:

* The user deselects all items.
* The user presses the Back button.
* The user taps **Done** (the left-arrow icon) on the left side of the action bar.
     
When _ActionMode_ is disabled, the contextual action bar disappears.

Follow these steps to create a contextual action bar, as shown in the figure below:
     
<br>
        <p align="center">
            <img  src="https://github.com/saisankar12/document/blob/master/saisankar_concept_images/dg_context_actionbar_design_pattern.png">
        </p>
 <br>
     
### Steps To Create ContextActionBar Menus:
     
1. Create an XML menu resource file for the menu items, and assign an icon to each one (as described in a previous section).
2. Set the long-click listener using [setOnLongClickListener()](https://developer.android.com/reference/android/view/View.html#setOnLongClickListener(android.view.View.OnLongClickListener)) to the View that should trigger the contextual action bar. Call [startActionMode()](https://developer.android.com/reference/android/app/Activity.html#startActionMode(android.view.ActionMode.Callback)) within the _setOnLongClickListener()_ method when the user performs a long tap on the View.
3. Implement the [ActionMode.Callback](https://developer.android.com/reference/android/view/ActionMode.Callback.html) interface to handle the _ActionMode_ lifecycle. Include in this interface the action for responding to a menu-item click in the [onActionItemClicked()](https://developer.android.com/reference/android/view/ActionMode.Callback.html#onActionItemClicked(android.view.ActionMode,%20android.view.MenuItem)) callback method.
4. Create a method to perform an action for each context menu item.
     
### Creating the XML resource file 
     
Create the XML menu resource directory and file by following the steps in the previous section on the options menu. Use a suitable name for the file, such as _menu_context_. Add icons for the context menu items. For example, the **Edit** menu item would have these attributes:
     
```xml
<item
   android:id="@+id/context_edit"
   android:orderInCategory="10"
   android:icon="@drawable/ic_action_edit_white"
   android:title="Edit" />
```
     
The standard contextual action bar has a dark background. Use a light or white color for the icons. If you are using clip art icons, choose **HOLO_DARK** for the **Theme** drop-down menu when creating the new image asset.
     
### Setting the long-click listener
     
Use [setOnLongClickListener()](https://developer.android.com/reference/android/view/View.html#setOnLongClickListener(android.view.View.OnLongClickListener)) to set a long-click listener to the _View_ that should trigger the contextual action bar. Add the code to set the long-click listener to the _Activity_ using the _onCreate()_ method. 

Follow these steps:

1. Declare the member variable mActionMode:
  
```java 
     private ActionMode mActionMode;
```
     
You will call [startActionMode()](https://developer.android.com/reference/android/app/Activity.html#startActionMode(android.view.ActionMode.Callback)) to enable [ActionMode](https://developer.android.com/reference/android/view/ActionMode.html), which returns the _ActionMode_ created. By saving this in a member variable _(mActionMode)_, you can make changes to the contextual action bar in response to other events.
     
2. Set up the contextual action bar listener in the _onCreate()_ method, using _View_ as the type in order to use the _setOnLongClickListener_ like below syantax:
     
```java
 @Override
 protected void onCreate(Bundle savedInstanceState) {
    // ... The rest of the onCreate code.
    Button b1 = findViewById(R.id.button); // Instead of Button you can write your own view
    b1.setOnLongClickListener(new View.OnLongClickListener()   
    {
       // Start ActionMode after long-click.
    });
 }
```
     
### Implementing the ActionMode.Callback interface
     
Before you can add the code to _onCreate()_ to start _ActionMode_, you must implement the [ActionMode.Callback](https://developer.android.com/reference/android/view/ActionMode.Callback.html) interface to manage the _ActionMode_ lifecycle. In its callback methods, you can specify the actions for the contextual action bar, and respond to clicks on action items.
     
1. Add the following method to the _Activity_ to implement the interface:
     
```java
 public ActionMode.Callback mActionModeCallback = new ActionMode.Callback() {
    // ... Code to create ActionMode.
 }
```
     
2. Add the _onCreateActionMode()_ code within the brackets of the above method to create ActionMode:
     
```java
 @Override
 public boolean onCreateActionMode(ActionMode mode, Menu menu) {
       // Inflate a menu resource providing context menu items
       MenuInflater inflater = mode.getMenuInflater();
       inflater.inflate(R.menu.menu_context, menu);
       return true;
 }
```
    
The [onCreateActionMode()](https://developer.android.com/reference/android/view/ActionMode.Callback.html#onCreateActionMode(android.view.ActionMode,%20android.view.Menu)) method inflates the menu using the same pattern used for a floating context menu. But this inflation occurs only when _ActionMode_ is created, which is when the user performs a long-click. The [MenuInflater](https://developer.android.com/reference/android/view/MenuInflater.html) class provides the [inflate()](https://developer.android.com/reference/android/view/MenuInflater.html#inflate(int,%20android.view.Menu)) method, which takes as a parameter the resource _id_ for an XML layout resource to load (_menu_context_ in the above example), and the [Menu](https://developer.android.com/reference/android/view/Menu.html) to inflate into (_menu_ in the above example).
     
3. Add the [onActionItemClicked()](https://developer.android.com/reference/android/view/ActionMode.Callback.html#onActionItemClicked(android.view.ActionMode,%20android.view.MenuItem)) method with your handlers for each menu item:
    
```java
     @Override
        public boolean onActionItemClicked(ActionMode mode, MenuItem item) {
            switch (item.getItemId()){
                case R.id.share:
                    Toast.makeText(ContextActionBarActivity.this, "You are Selected"+item.getTitle(), Toast.LENGTH_SHORT).show();
                    mode.finish();
                    break;
                case R.id.edit:
                    mode.finish();
                    break;
                case R.id.delete:
                    mode.finish();
                    break;
            }
            return false;
        }
```
     
The above code above uses the [getItemId()](https://developer.android.com/reference/android/view/MenuItem.html#getItemId()) method to get the _id_ for the selected menu item, and uses it in a _switch case_ block to determine which action to take. The _id_ in each _case_ statement is the _android:id_ attribute assigned to the menu item in the XML menu resource file.

The actions shown are the _editNote()_ and _shareNote()_ methods, which you create in the Activity. After the action is picked, you use the mode.finish() method to close the contextual action bar.
     
4. Add the [onPrepareActionMode()](https://developer.android.com/reference/android/view/ActionMode.Callback.html#onPrepareActionMode(android.view.ActionMode,%20android.view.Menu)) and [onDestroyActionMode()](https://developer.android.com/reference/android/view/ActionMode.Callback.html#onDestroyActionMode(android.view.ActionMode)) methods, which manage the ActionMode lifecycle:
     
 ```java
 @Override
 public boolean onPrepareActionMode(ActionMode mode, Menu menu) {
       return false; // Return false if nothing is done.
 }
```
     
The _onPrepareActionMode()_ method shown above is called each time _ActionMode_ occurs, and is always called after _onCreateActionMode()_.
     
```java
@Override
public void onDestroyActionMode(ActionMode mode) {
   mActionMode = null;
}
```
     
The _onDestroyActionMode()_ method shown above is called when the user exits _ActionMode_ by clicking **Done** in the contextual action bar, or clicking on a different view.
     
The following is the full code for the [ActionMode.Callback](https://developer.android.com/reference/android/view/ActionMode.Callback.html) interface implementation:
     
```java
private ActionMode.Callback callback = new ActionMode.Callback() {
        @Override
        public boolean onCreateActionMode(ActionMode mode, Menu menu) {
            mode.getMenuInflater().inflate(R.menu.menu, menu);
            return true;
        }
        // Called each time ActionMode is shown. Always called after onCreateActionMode.
        @Override
        public boolean onPrepareActionMode(ActionMode mode, Menu menu) {
            return false;
        }
        // Called when the user selects a contextual menu item
        @Override
        public boolean onActionItemClicked(ActionMode mode, MenuItem item) {
            switch (item.getItemId()) {
                case R.id.share:
                    Toast.makeText(ContextActionBarActivity.this, "You are Selected" + item.getTitle(), Toast.LENGTH_SHORT).show();
                    mode.finish();
                    break;
                case R.id.edit:
                    mode.finish();
                    break;
                case R.id.delete:
                    mode.finish();
                    break;
            }
            return false;
        }
        // Called when the user exits the action mode
        @Override
        public void onDestroyActionMode(ActionMode mode) {
            mActionMode = null;
        }
    };
```
     
### Starting ActionMode
     
You use [startActionMode()](https://developer.android.com/reference/android/app/Activity.html#startActionMode(android.view.ActionMode.Callback)) to start _ActionMode_ after the user performs a long-click.

To start _ActionMode_, add the _onLongClick()_ method within the brackets of the _setOnLongClickListener_ method in _onCreate()_ below syntax:
     
```java
@Override
protected void onCreate(Bundle savedInstanceState) {
   // ... Rest of onCreate code
   b1.setOnLongClickListener(new View.OnLongClickListener() {
      // Called when the user long-clicks on articleView
      public boolean onLongClick(View view) {
         if (mActionMode != null) return false;
         // Start the contextual action bar
         // using the ActionMode.Callback.
         mActionMode = 
               MainActivity.this.startActionMode(callback);
         view.setSelected(true);
         return true;
      }
   });
}
```
     
The above code first ensures that the _ActionMode_ instance is not recreated if it's already active by checking whether _mActionMode_ is _null_ before starting the action mode:
     
```java
     if (mActionMode != null) return false;
```
     
When the user performs a long-click, the call is made to _startActionMode()_ using the _ActionMode.Callback_ interface, and the contextual action bar appears at the top of the display. The [setSelected()](https://developer.android.com/reference/android/view/View.html#setSelected(boolean)) method changes the state of this _View_ to selected (set to _true_).
     
The following is the code for the _onCreate()_ method in the _Activity_, which now includes _setOnLongClickListener()_ and _startActionMode()_:
     
```java
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.design);
        Button b1 = findViewById(R.id.button);
        b1.setOnLongClickListener(new View.OnLongClickListener() {
            @Override
            public boolean onLongClick(View v) {
                if (mActionMode != null) {
                    return false;
                }
                // Start the contextual action bar using the ActionMode.Callback.
                mActionMode = ContextActionBarActivity.this.startActionMode(callback);
                return true;
            }
        });
    }
```
    
## Popup menu
     
A [PopupMenu](https://developer.android.com/reference/android/widget/PopupMenu.html) is a vertical list of items anchored to a [View](https://developer.android.com/reference/android/view/View.html). It appears below the anchor _View_ if there is room, or above the _View_ otherwise.

A popup menu is typically used to provide an overflow of actions (similar to the overflow action icon for the options menu) or the second part of a two-part command. Use a popup menu for extended actions that relate to regions of content in your _Activity_. Unlike a context menu, a popup menu is anchored to a _Button_, is always available, and its actions generally do not affect the content of the _View_.

For example, the Gmail app uses a popup menu anchored to the overflow icon in the app bar when showing an email message. The popup menu items **Reply
**, **Reply All**, and **Forward** are related to the email message, but don't affect or act on the message. Actions in a popup menu should not directly affect the corresponding content (use a contextual menu to directly affect selected content). As shown below, a popup can be anchored to the overflow action button in the app bar.
    
<br>
 <p align="center">
    <img  src="https://github.com/saisankar12/document/blob/master/saisankar_concept_images/dg_popupmenu.png">
 </p>
<br>

### Creating a popup menu
    
Follow these steps to create a popup menu (refer to figure below):

<br>
 <p align="center">
    <img  src="https://github.com/saisankar12/document/blob/master/saisankar_concept_images/dg_popup_menu_design_pattern.png">
 </p>
<br>
    
### Steps to Implement PopUp Menu:
    
1. Create an XML menu resource file for the popup menu items, and assign appearance and position attributes (as described in a previous section).
2. Add an [Button](https://developer.android.com/reference/android/widget/Button.html) for the popup menu icon in the XML activity layout file.
3. Assign [onClickListener()](https://developer.android.com/reference/android/view/View.OnClickListener.html) to the _Button_.
4. Override the _onClick()_ method to inflate the popup menu and register it with [PopupMenu.OnMenuItemClickListener](https://developer.android.com/reference/android/widget/PopupMenu.OnMenuItemClickListener.html).
5. Implement the [onMenuItemClick()](https://developer.android.com/reference/android/view/MenuItem.OnMenuItemClickListener.html#onMenuItemClick(android.view.MenuItem)) method.
6. Create a method to perform an action for each popup menu item.
    
Create the XML menu resource directory and file by following the steps in a previous section. Use a suitable name for the file, such as _menu_popup_.
    
<br>
 <p align="center">
    <img  src="https://github.com/saisankar12/document/blob/master/saisankar_concept_images/popup_menu_settings_favorites.png">
 </p>
<br>
    
### Adding an ImageButton for the icon to click
    
Use an [Button](https://developer.android.com/reference/android/widget/Button.html) in the _Activity_ layout for the icon that triggers the popup menu. Popup menus are anchored to a _View_ in the _Activity_, such as an ImageButton. The user clicks it to see the menu.
    
```xml
    <Button
        android:id="@+id/button"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Pop Up Menu"/>
```
    
### Assigning onClickListener to the button
    
1. Create a member variable (mButton) in the Activity class definition:
    
```java
    public class MainActivity extends AppCompatActivity {
    private Button mButton;
    // ... Rest of Activity code
 }
```    
    
2. In the _onCreate()_ method for the same _Activity_, assign _onClickListener()_ to the Button:
    
```java
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_popup_menu);
        b1= findViewById(R.id.button);
        b1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
               // Implement PopMenu Here
            }
        });
    }
```
    
### Inflating the popup menu
    
As part of the _setOnClickListener()_ method within _onCreate()_, add the onClick() method to inflate the popup menu and register it with [PopupMenu.OnMenuItemClickListener](https://developer.android.com/reference/android/widget/PopupMenu.OnMenuItemClickListener.html):
    
```java
        b1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                PopupMenu popupMenu=new PopupMenu(PopupMenuActivity.this,b1);
                popupMenu.getMenuInflater().inflate(R.menu.menu,popupMenu.getMenu());
                
                popupMenu.show();
            }
        });
    }
```
    
The method instantiates a [PopupMenu](https://developer.android.com/reference/android/widget/PopupMenu.html) object, which is _popup_ in the example above. Then the method uses the [MenuInflater](https://developer.android.com/reference/android/view/MenuInflater.html) class and its [inflate()](https://developer.android.com/reference/android/view/MenuInflater.html#inflate(int,%20android.view.Menu)) method.

The _inflate()_ method takes the following parameters:

* The resource _id_ for an XML layout resource to load, which is _menu_popup_ in the example above.
* The [Menu](https://developer.android.com/reference/android/view/Menu.html) to inflate into, which is _popup.getMenu()_ in the example above.
    
The code then registers the popup with the listener, [PopupMenu.OnMenuItemClickListener](https://developer.android.com/reference/android/widget/PopupMenu.OnMenuItemClickListener.html).
    
### Implementing onMenuItemClick
    
To perform an action when the user selects a popup menu item, implement the [onMenuItemClick()](https://developer.android.com/reference/android/widget/PopupMenu.OnMenuItemClickListener.html#onMenuItemClick(android.view.MenuItem)) callback within the above _setOnClickListener()_ method. Finish the method with _popup.show_ to show the popup menu:
    
```java
       b1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                PopupMenu popupMenu=new PopupMenu(PopupMenuActivity.this,b1);
                popupMenu.getMenuInflater().inflate(R.menu.menu,popupMenu.getMenu());
                popupMenu.setOnMenuItemClickListener(new PopupMenu.OnMenuItemClickListener() {
                    @Override
                    public boolean onMenuItemClick(MenuItem item) {
                        switch (item.getItemId()){
                            case R.id.share:
                                Toast.makeText(PopupMenuActivity.this, "Share", Toast.LENGTH_SHORT).show();
                                break;
                        }
                        return false;
                    }
                });
                popupMenu.show();
            }
        });
```
   
### The PopupMenu Output Shown Below:
    
<br>
 <p align="center">
    <img  src="https://github.com/saisankar12/document/blob/master/saisankar_concept_images/pop_up_menu_output.jpg">
 </p>
<br>    
    
