## Room, LiveData, and ViewModel

##### What are Android Architecture Components?

<br>
<p align="center">
<img  src="https://github.com/mastan511/MastanImages/blob/master/architecture_components_logo.png?raw=true" width = "250dp">
</p>
<br>

The Android OS manages resources aggressively to perform well on a huge range of devices, and sometimes that makes it challenging to build robust apps. [Android Architecture Components](https://developer.android.com/topic/libraries/architecture/index.html) provide guidance on app architecture, with libraries for common tasks like lifecycle management and data persistence.

Architecture Components help you structure your app in a way that is robust, testable, and maintainable with less boilerplate code. Architecture Components provide a simple, flexible, and practical approach that frees you from some common problems so you can focus on building great experiences.

### Recommended Architecture Components

To introduce the terminology, here is a short introduction to the Architecture Components and how they work together. Each component is explained more in the following sections. This diagram shows a basic form of this architecture.

<br>
<p align="center">
<img  src="https://github.com/mastan511/MastanImages/blob/master/dg_architecture_comonents.png?raw=true">
</p>
<br>

* **_Entity_**: When working with Architecture Components, the entity is an annotated class that describes a database table.

* **_SQLite database_**: On the device, data is stored in an SQLite database. For simplicity, additional storage options, such as a web server, are omitted from this chapter. The [Room persistence library](https://developer.android.com/training/data-storage/room/index.html) creates and maintains this database for you.

* **_DAO_**: Data access object. A mapping of SQL queries to functions. You used to have to define these queries in a helper class, such as [SQLiteOpenHelper](https://developer.android.com/reference/android/database/sqlite/SQLiteOpenHelper.html). When you use a DAO, you call the methods, and the components take care of the rest.

* **_Room database_**: Database layer on top of SQLite database that takes care of mundane tasks that you used to handle with a helper class, such as SQLiteOpenHelper. Provides easier local data storage. The Room database uses the DAO to issue queries to the SQLite database.

* **_Repository_**: A class that you create for managing multiple data sources, for example using the WordRepository class.

* **_ViewModel_**: Provides data to the UI and acts as a communication center between the Repository and the UI. Hides the backend from the UI. ViewModel instances survive device configuration changes.

* **_LiveData_**: A data holder class that follows the [observer pattern](https://en.wikipedia.org/wiki/Observer_pattern), which means that it can be observed. Always holds/caches latest version of data. Notifies its observers when the data has changed. LiveData is lifecycle aware. UI components observe relevant data. LiveData automatically manages stopping and resuming observation, because it's aware of the relevant lifecycle status changes.

##### RoomWordSample architecture overview

The following diagram shows the same basic architecture form as the diagram above, but in the context of an app. The following sections delve deeper into each component.

<br>
<p align="center">
<img  src="https://github.com/mastan511/MastanImages/blob/master/dg_app_architecture.png?raw=true">
</p>
<br>

##### Implementation Practical:

##### Gradle files

To use the Architecture Components libraries, you must manually add the latest version of the libraries to your Gradle files.

Add the following code to your build.gradle (Module: app) file, at the end of the dependencies block and Sync Now:

```gradle
    // Room components
    implementation "androidx.room:room-runtime:2.2.1"
    annotationProcessor "androidx.room:room-compiler:2.2.1"
    androidTestImplementation "androidx.room:room-testing:2.2.1"

    // Lifecycle components
    implementation "androidx.lifecycle:lifecycle-extensions:2.2.0"
    annotationProcessor "androidx.lifecycle:lifecycle-compiler:2.2.0"
```

##### Entity

The data for an app with a database centers around the data stored in the database. Of course, there can be other data from different sources, but for simplicity, this discussion ignores other data.

<br>
<p align="center">
<img  src="https://github.com/mastan511/MastanImages/blob/master/dg_app_architecture_entity.png?raw=true">
</p>
<br>

Room models an SQLite database, and is implemented with an SQLite database as its backend. SQLite databases store their data in tables of rows and columns. Each row represents one entity (or record), and each column represents a value in that entity. For example, an entity for a dictionary entry might include a unique ID, the word, a definition, grammatical information, and links to more info.

Another common entity is for a person, with a unique ID, first name, last name, email address, and demographic information. The entities in such a database might look like this:


| ID  | First name| Last name |
| ------------- | ------------- | ------- |
| 12345  | Sai  | Sankar|
| 12346 | Masthan  | Vali |

When you write an app using Architecture Components (or an SQLite database), you define your entity or entities in classes. Each instance of the class represents a row, and each column is represented by a member variable.

Here is code representing a Person entity:

```java
public class Student {
    String rollNumber;
    String Mailid;
    String phoneNumber;
    String name;
}
```

##### Entity annotations

For Room to work with an entity, you need to give Room information that relates the contents of the entity's Java class (for example Person) to what you want to represent in the database table. You do this using annotations.

Here are some commonly used annotations:

* _@Entity(tableName ="word_table")_ Each @Entity instance represents an entity in a table. Specify the name of the table if you want it to be different from the name of the class.
* _@PrimaryKey_ Every entity needs a primary key. To [_auto-generate_](https://developer.android.com/reference/android/arch/persistence/room/PrimaryKey.html) a unique key for each entity, add and annotate a primary integer key with autoGenerate=true, as shown in the code below. See [Defining data using Room entities].
* @NonNull Denotes that a parameter, field, or method return value can never be null. The primary key should always use the @NonNull annotation. Use this annotation for mandatory fields in your rows.
* @ColumnInfo(name ="word") Specify the name of the column in the table, if you want the column name to be different from the name of the member variable.

Every field that's stored in the database must either be public or have a "getter" method so that Room can access it. The code below provides a getWord() "getter" method rather than exposing member variables directly.

Here is annotated code representing a _Student_ entity:

```java
@Entity(tableName = "StudentInfo")
public class Student {

    @PrimaryKey @NonNull
    String rollNumber;

    @ColumnInfo(name = "StudentMailId")
    String Mailid;
    String phoneNumber;

    @ColumnInfo(name = "StudentName")
    String name;
}
```
You can also use annotations to define relationships between entities. For details and a complete list of annotations, see the Room package summary reference.

##### The DAO (data access object)

To access your app's data using the Room persistence library, you work with data access objects, or DAOs. A set of Dao objects (DAOs) forms the main component of a Room database. Each DAO includes methods that offer abstract access to your app's database.

<br>
<p align="center">
<img  src="https://github.com/mastan511/MastanImages/blob/master/dg_app_architecture_dao.png?raw=true">
</p>
<br>

You annotate the DAO to specify SQL queries and associate them with method calls. The compiler checks the SQL for errors, then generates queries from the annotations. For common queries, the libraries provide convenience annotations, such as _@Insert, @Delete, and @Update_.

Note that:

* The DAO must be an interface or abstract class.
* Room uses the DAO to create a clean API for your code.
* By default, queries (@Query) must be executed on a thread other than the main thread. For operations such as inserting or deleting, Room takes care of thread management for you if you use the appropriate annotations.
* The default action when you ask Room to insert an entity that is already in the database is to ABORT. You can specify a different conflict strategy, such as REPLACE.

```java
@Dao
public interface StudentDao {

    @Insert
    public void insert(Student student);

    @Delete
    public void delete(Student student);

    @Query("SELECT * FROM StudentInfo")
    List<Student> readData();
    
    // Query with parameter that returns a specific word or words.
   @Query("SELECT * FROM word_table WHERE word LIKE :word ")
   public List<Word> findWord(String word);
}
```
Learn more about [Room DAOs](https://developer.android.com/training/data-storage/room/accessing-data.html).

##### LiveData

When your app displays data or uses data in other ways, you usually want to take action when the data changes. This means your app has to observe the data so that when it changes, the app can react. Depending on how the data is stored, this can be tricky. Observing changes to data across multiple components of your app can create explicit, rigid dependency paths between the components. This makes testing and debugging, among other things, difficult.

<br>
<p align="center">
<img  src="https://github.com/mastan511/MastanImages/blob/master/dg_app_architecture_livedata.png?raw=true">
</p>
<br>

To avoid these problems, use LiveData, which is a [lifecycle library](https://developer.android.com/topic/libraries/architecture/lifecycle.html) class for data observation. If you use a return value of type [LiveData](https://developer.android.com/reference/android/arch/lifecycle/LiveData.html) in your method description, Room generates all necessary code to update the LiveData when the database is updated.

##### Benefits of using LiveData

_Ensures that your UI matches your data state_

LiveData follows the [observer pattern](https://en.wikipedia.org/wiki/Observer_pattern), so it notifies [Observer](https://developer.android.com/reference/android/arch/lifecycle/Observer.html) objects when the lifecycle state changes. You can consolidate your code to update the UI within these observer objects. Instead of updating the UI every time the app data changes, your observer can update the UI every time there's a state change.

_No memory leaks_

Observers are bound to [Lifecycle](https://developer.android.com/reference/android/arch/lifecycle/Lifecycle.html) objects, and the observers clean up after themselves when their associated lifecycle is destroyed.

_No crashes due to stopped activities_

If the observer's lifecycle is inactive, as in the case of an activity in the back stack, then it doesn't receive any LiveData events.

_No more manual lifecycle handling_

UI components just observe relevant data and don't stop or resume observation. LiveData is aware of relevant lifecycle status changes while observing, so LiveData automatically manages stopping and resuming observation.

_Data is always up-to-date_

If a lifecycle becomes inactive, it receives the latest data upon becoming active again. For example, an activity that was in the background receives the latest data right after it returns to the foreground.

_Configuration changes handled properly_

If an activity or fragment is re-created due to a configuration change, like device rotation, the activity or fragment immediately receives the latest available data.

_Resources can be shared_

You can extend a LiveData object using the [singleton](https://en.wikipedia.org/wiki/Singleton_pattern) pattern. Do this, for example, for services or a database. The LiveData object connects to the system service once, and then any observer that needs the resource can just watch the LiveData object. For more information, see Extend [LiveData](https://developer.android.com/topic/libraries/architecture/livedata.html#extend_livedata).

##### Using LiveData

Follow these general steps to work with LiveData objects:

1. Create an instance of [LiveData](https://developer.android.com/topic/libraries/architecture/livedata.html#extend_livedata). to hold a certain type of data. This is usually done within your [ViewModel](https://developer.android.com/reference/android/arch/lifecycle/ViewModel.html) class.
2. Create an [Observer](https://developer.android.com/reference/android/arch/lifecycle/Observer.html) object that defines the [onChanged()](https://developer.android.com/reference/android/arch/lifecycle/Observer.html#onChanged(T)) method, which controls what happens when the LiveData object's held data changes. You usually create an Observer object in a UI controller, such as an activity or fragment.
3. Attach the Observer object to the LiveData object using the [observe()](https://developer.android.com/reference/android/arch/lifecycle/LiveData.html#observe(android.arch.lifecycle.LifecycleOwner,%20%20%20android.arch.lifecycle.Observer%3CT%3E)) method. The observe() method takes a LifecycleOwner object. This subscribes the Observer object to the LiveData object so that the observer is notified of changes. You usually attach the Observer object in a UI controller, such as an activity or fragment.

**Note:** You can register an observer without an associated [LifecycleOwner](https://developer.android.com/reference/android/arch/lifecycle/LifecycleOwner.html) object using the [observeForever(Observer)](https://developer.android.com/reference/android/arch/lifecycle/LiveData.html#observeForever(android.arch.lifecycle.Observer%3CT%3E)) method. In this case, the observer is considered to be always active and is therefore always notified about modifications. To remove these observers, call the removeObserver(Observer) method.

When you update the value stored in the LiveData object, all registered observers are notified and will take specified actions, such as updating the UI, as long as the attached LifecycleOwner is in the active state.

LiveData allows UI-controller observers to subscribe to updates. When the data held by the LiveData object changes, the UI automatically updates in response.

These steps are explained in more detail in the rest of this chapter.

##### Making data observable with LiveData

To make data observable, wrap it with LiveData. That's it.

For the Person example, in the DAO you would wrap the returned data into LiveData, as shown in this code:

```xml
@Query("SELECT * FROM StudentInfo")
    LiveData<List<Student>> readData();
```

**Important:** When you pass data through the layers of your app architecture from a Room database to your UI, that data has to be LiveData in all layers: All the data that Room returns to the Repository, and the Repository then passes to the ViewModel, must be LiveData. You can then create an observer in the activity that observes the data in the ViewModel.

### MutableLiveData

You can use LiveData independently from Room, but to do so you must manage data updates. However, LiveData has no publicly available methods to update the stored data.

Therefore, if you want to update the stored data, you must use [MutableLiveData](https://developer.android.com/reference/android/arch/lifecycle/MutableLiveData.html) instead of LiveData. The MutableLiveData class adds two public methods that allow you to set the value of a LiveData object: [setValue(T)](https://developer.android.com/reference/android/arch/lifecycle/MutableLiveData.html#setValue(T)) and [postValue(T)](https://developer.android.com/reference/android/arch/lifecycle/MutableLiveData.html#postValue(T)).

MutableLiveData is usually used in the ViewModel, and then the [ViewModel](https://developer.android.com/reference/android/arch/lifecycle/ViewModel.html) only exposes immutable LiveData objects to the observers.

See the Architecture Components' [BasicSample](https://github.com/android/architecture-components-samples/tree/master/BasicSample) code for examples of using MutableLiveData. The example in [Guide to App Architecture](https://developer.android.com/topic/libraries/architecture/guide.html) also shows a use MutableLiveData.


##### Observing LiveData

To update the data that is shown to the user, create an observer of the data in the onCreate() method of MainActivity and override the observer's onChanged() method. When the LiveData changes, the observer is notified and onChanged() is executed. You then update the cached data, for example in the adapter, and the adapter updates what the user sees.

Usually you observe data in a ViewModel, not directly in the Repository or in Room. ViewModel is described in a later section.

The following code synatx shows how to attach an observer to LiveData:
```java
// Create the observer which updates the UI.
final Observer<String> nameObserver = new Observer<String>() {
    @Override
    public void onChanged(@Nullable final String newName) {
        // Update the UI, in this case, a TextView.
        mNameTextView.setText(newName);
    }
};

mModel.getCurrentName().observe(this, nameObserver);
```

See the LiveData documentation to learn other ways to use LiveData, or watch this [Architecture Components: LiveData and Lifecycle video](https://www.youtube.com/watch?v=jCw5ib0r9wg).

### Room database

Room is a database layer on top of an SQLite database. Room takes care of mundane tasks that you used to handle with an [SQLiteOpenHelper](https://developer.android.com/reference/android/database/sqlite/SQLiteOpenHelper.html).

<br>
<p align="center">
<img  src="https://github.com/mastan511/MastanImages/blob/master/dg_app_architecture_roomdb.png?raw=true">
</p>
<br>

To use Room:

1. Create a public abstract class that extends RoomDatabase.
2. Use annotations to declare the entities for the database and set the version number.
3. Use Room's database builder to create the database if it doesn't exist.
4. Add a migration strategy for the database. When you modify the database schema, you'll need to update the version number and define how to handle migrations. For a sample, destroying and re-creating the database is a fine migration strategy. For a real app, you must implement a migration strategy. See [Understanding migrations with Room](https://medium.com/androiddevelopers/understanding-migrations-with-room-f01e04b07929).

Note that:

* Room provides compile-time checks of SQLite statements.
* By default, to avoid poor UI performance, Room doesn't allow you to issue database queries on the main thread. LiveData applies this rule by automatically running the query asynchronously on a background thread, when needed.
* Usually, you only need one instance of the Room database for the whole app. Make your RoomDatabase a singleton to prevent having multiple instances of the database opened at the same time, which would be a bad thing.

Here is a sample of a complete Room class:
```java
@Database(entities = {Student.class} , version = 1 , exportSchema = false)
public abstract class StudentDataBase extends RoomDatabase {

    public abstract StudentDao myDao();

    private static StudentDataBase dataBase;

    static synchronized StudentDataBase getDataBase(Context context){
        if (dataBase == null){
            dataBase = Room.databaseBuilder(context,
                    StudentDataBase.class,"MyDb")
                    .allowMainThreadQueries()
                    .fallbackToDestructiveMigration().build();
        }
        return dataBase;
    }
}
```
##### Repository

A Repository is a class that abstracts access to multiple data sources. The Repository is not part of the Architecture Components libraries, but is a suggested best practice for code separation and architecture. A Repository class handles data operations. It provides a clean API to the rest of the app for app data.

<br>
<p align="center">
<img  src="https://github.com/mastan511/MastanImages/blob/master/dg_app_architecture_repository.png?raw=true">
</p>
<br>

A Repository is where you would put the code to manage query threads and use multiple backends, if appropriate. Once common use for a Repository is to implement the logic for deciding whether to fetch data from a network or use results cached in the database.

<br>
<p align="center">
<img  src="https://github.com/mastan511/MastanImages/blob/master/dg_repository.png?raw=true">
</p>
<br>

Here is the complete code for a basic Repository:
```java
public class StudentRepository {

    private StudentDataBase studentDataBase;
    private LiveData<List<Student>> read;

    StudentRepository(Application application) {
        studentDataBase=StudentDataBase.getDataBase(application);
        read = studentDataBase.myDao().readData();
    }

    void insertData(Student student){
        new InsertTask().execute(student);
    }
    void deleteData(Student student){
        new DeleteTask().execute(student);
    }

    LiveData<List<Student>> readData(){
        return read;
    }
    
    class  InsertTask extends AsyncTask<Student,Void,Void>{
        @Override
        protected Void doInBackground(Student... students) {
            studentDataBase.myDao().insert(students[0]);
            return null;
        }
    }

    class DeleteTask extends AsyncTask<Student,Void,Void>{
        @Override
        protected Void doInBackground(Student... students) {
            studentDataBase.myDao().delete(students[0]);
            return null;
        }
    }
}
```
**Note**: In this example, the Repository doesn't do much. See the [BasicSample](https://github.com/android/architecture-components-samples/tree/master/BasicSample) for an applied implementation.

The [Guide to App Architecture] includes a more complex example that uses a web service to fetch data.

##### ViewModel

The ViewModel is a class whose role is to provide data to the UI and survive configuration changes. A ViewModel acts as a communication center between the Repository and the UI. You can also use a ViewModel to share data between fragments. The ViewModel is part of the [lifecycle library](https://developer.android.com/topic/libraries/architecture/lifecycle.html). For an introductory guide to this topic, see the ViewModel overview.

<br>
<p align="center">
<img  src="https://github.com/mastan511/MastanImages/blob/master/dg_app_architecture_viewmodel.png?raw=true">
</p>
<br>

A ViewModel holds your app's UI data in a lifecycle-conscious way that survives configuration changes. Separating your app's UI data from your Activity and Fragment classes lets you better follow the single responsibility principle: Your activities and fragments are responsible for drawing data to the screen, while your ViewModel is responsible for holding and processing all the data needed for the UI.

<br>
<p align="center">
<img  src="https://github.com/mastan511/MastanImages/blob/master/dg_view_model.png?raw=true">
</p>
<br>

**Warning:** Never pass context into ViewModel instances. Do not store Activity, Fragment, or View instances or their Context in the ViewModel. An Activity can be destroyed and created many times during the lifecycle of a ViewModel, such as when the device is rotated. If you store a reference to the Activity in the ViewModel, you end up with references that point to the destroyed Activity. This is a memory leak. If you need the application context, use AndroidViewModel instead of ViewModel.

In the ViewModel, use LiveData for changeable data that the UI will use or display, so that you can add an observer and respond to changes.

Here is the complete code for a sample ViewModel:
```java
public class StudentViewModel extends AndroidViewModel {

    private StudentRepository repository;
    private LiveData<List<Student>> readAllData;
    public StudentViewModel(@NonNull Application application) {
        super(application);
        repository = new StudentRepository(application);
        readAllData = repository.readData();
    }

    void insert(Student student){
        repository.insertData(student);
    }

    void delete(Student student){
        repository.deleteData(student);
    }

    LiveData<List<Student>> readData(){
        return readAllData;
    }
}
```
**Important:** ViewModel is not a replacement for onSaveInstanceState(), because the ViewModel does not survive a process shutdown. See [Saving UI States](https://developer.android.com/topic/libraries/architecture/saving-states.html).

To learn more, watch this [Architecture Components: ViewModel video](https://www.youtube.com/watch?v=c9-057jC1ZA).

### Displaying LiveData

Finally, you can display all this interesting data to the user.

<br>
<p align="center">
<img  src="https://github.com/mastan511/MastanImages/blob/master/dg_app_architecture_UI.png?raw=true">
</p>
<br>

Whenever the data changes, the onChanged() method of your observer is called.

In the most basic case, this can update the contents of a TextView, as shown in this code:
```java
final Observer<String> nameObserver = new Observer<String>() {
    @Override
    public void onChanged(@Nullable final String newName) {
        // Update the UI, in this case, a TextView.
        mNameTextView.setText(newName);
    }
};
```
Another common case is to display data in a View that works with an adapter. For example, if you are showing data in a RecyclerView, the onChanged() method updates the data cached in the adapter:
```java
        viewModel.readData().observe(this, new Observer<List<Student>>() {
            @Override
            public void onChanged(List<Student> students) {
                rv.setLayoutManager(new LinearLayoutManager(MainActivity.this));
                rv.setAdapter(new MyDataAdapter(MainActivity.this,students));
            }
        });
```

**Tip**: One way to get a reference to the application context in a data repository is to extend the Application class and add a member of type Context to that custom subclass.

##### Lifecycle-aware components

Most of the app components that are defined in the Android framework have lifecycles attached to them. Lifecycles are managed by the operating system or the framework code running in your process. They are core to how Android works and your app must respect them. Not doing so may trigger memory leaks or even app crashes. Activities and fragments are examples of lifecycle-aware components, and LiveData is lifecycle aware.

A common pattern is to implement the actions of the dependent components in the lifecycle methods of activities and fragments. For example, you might have a listener class that connects to a service when the activity starts, and disconnects when the activity is stopped. In the activity, you then override the onStart() and onStop() methods to start and stop the listener.

```java
@Override
    public void onStart() {
        super.onStart();
        myListener.start();
}
```
This code snippet looks innocent enough. However, once you have multiple components, using this pattern leads to poor code organization and a proliferation of errors, such as possible race conditions.

Lifecycle-aware components perform actions in response to a change in the lifecycle status of another component. For example, a listener could start and stop itself in response to an activity starting and stopping. This results in code that is better-organized, usually shorter, and always easier to maintain.

The android.arch.lifecycle package provides classes and interfaces that let you build lifecycle-aware components that automatically adjust their behavior based on the lifecycle state of an activity or fragment. That is, you can make any class lifecycle aware.

* To import android.arch.lifecycle into your Android project, see [Adding Components to your Project](https://developer.android.com/topic/libraries/architecture/adding-components.html).
* See [Handling Lifecycles with Lifecycle-Aware Components](https://developer.android.com/topic/libraries/architecture/lifecycle.html) for more details on using these components.
    
##### Use cases for lifecycle-aware components

Lifecycle-aware components can make it much easier for you to manage lifecycles in a variety of cases. For example, you can use lifecycle-aware components to:

* Switch between coarse and fine-grained location updates.

  Use lifecycle-aware components to enable fine-grained location updates while your location app is visible, then switch to coarse-grained updates when the app is in the           background. Add LiveData to automatically update the UI when your user changes locations.
  
* Stop and start video buffering.

Use lifecycle-aware components to start video buffering as soon as possible, but defer playback until the app is fully started. You can also use lifecycle-aware components to end buffering when your app is destroyed.

* nStart and stop network connectivity.

Use lifecycle-aware components to enable live updating (streaming) of network data while an app is in the foreground, then automatically pause when the app moves into the background.

* Pause and resume animated drawables.

Use lifecycle-aware components to pause animated drawables while the app is in the background, then resume drawables after the app returns to the foreground.

##### Practical Example:

**activity_main.xml**
```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:padding="20dp"
    tools:context=".MainActivity">
    
    <com.google.android.material.floatingactionbutton.FloatingActionButton
        android:id="@+id/fab"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:src="@drawable/ic_person_add_black_24dp"
        app:layout_constraintBottom_toBottomOf="@+id/recycler"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.954"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.96" />
    
    <androidx.recyclerview.widget.RecyclerView
        android:id="@+id/recycler"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>
```

**MainActivity.java**

```java
public class MainActivity extends AppCompatActivity {

    FloatingActionButton fab;
    RecyclerView rv;
    static StudentViewModel viewModel;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        fab=findViewById(R.id.fab);
        rv =findViewById(R.id.recycler);

        fab.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent i = new Intent(MainActivity.this,InsertActivity.class);
                startActivity(i);
            }
        });

        viewModel = ViewModelProviders.of(MainActivity.this)
                .get(StudentViewModel.class);

        viewModel.readData().observe(MainActivity.this, new Observer<List<Student>>() {
            @Override
            public void onChanged(List<Student> students) {
                rv.setLayoutManager(new LinearLayoutManager(MainActivity.this));
                rv.setAdapter(new MyDataAdapter(MainActivity.this,students));
            }
        });
    }
}
```
**activity_insert.xml**

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="10dp"
    tools:context=".InsertActivity">

    <EditText
        android:id="@+id/studentname"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter Student Name"
        android:inputType="text" />

    <EditText
        android:id="@+id/studentrollnumber"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter RollNumber"
        android:inputType="text" />

    <EditText
        android:id="@+id/studentmailid"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter Mail ID"
        android:inputType="textEmailAddress" />

    <EditText
        android:id="@+id/studentmobileNumber"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter Mobile Number"
        android:inputType="phone" />

    <Button
        android:id="@+id/save"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center"
        android:onClick="save"
        android:text="Save" />
</LinearLayout>
```

**InsertActivity.java**

```java
public class InsertActivity extends AppCompatActivity {

    EditText sname, sroll, smobile, smail;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_insert);

        sname = findViewById(R.id.studentname);
        sroll = findViewById(R.id.studentrollnumber);
        smail = findViewById(R.id.studentmailid);
        smobile = findViewById(R.id.studentmobileNumber);
    }
    public void save(View view) {
        String name = sname.getText().toString();
        String mailid = smail.getText().toString();
        String phone = smobile.getText().toString();
        String roll = sroll.getText().toString();

        Student student = new Student();
        student.setName(name);
        student.setMailID(mailid);
        student.setMobileNUmber(phone);
        student.setRollNumber(roll);

        MainActivity.viewModel.insert(student);

        finish();
    }
}
```

**row_design.xml**

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="vertical"
    android:padding="10dp">

    <TextView
        android:id="@+id/readname"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:fontFamily="serif"
        android:text="Name"
        android:textColor="#E91E63"
        android:textSize="20sp" />

    <TextView
        android:id="@+id/readroll"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="5dp"
        android:fontFamily="serif"
        android:text="RollNumber"
        android:textColor="#3F51B5"
        android:textSize="20sp" />

    <TextView
        android:id="@+id/readMailid"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="5dp"
        android:fontFamily="serif"
        android:text="Mail ID"
        android:textColor="#BF3205"
        android:textSize="20sp" />

    <TextView
        android:id="@+id/readmobile"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="5dp"
        android:fontFamily="serif"
        android:text="RollNumber"
        android:textColor="#039109"
        android:textSize="20sp" />

    <ImageView
        android:id="@+id/delete"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="end"
        android:contentDescription="Delete"
        android:src="@drawable/ic_delete_forever_black_24dp" />

    <View
        android:layout_width="match_parent"
        android:layout_height="1dp"
        android:layout_marginTop="5dp"
        android:background="#2196F3" />

</LinearLayout>
```

**MyDataAdapter.java**

```java
public class MyDataAdapter extends RecyclerView.Adapter<MyDataAdapter.DataViewHolder> {

    Context ct;
    List<Student> students;

    public MyDataAdapter(MainActivity mainActivity, List<Student> studentList) {
        ct = mainActivity;
        students = studentList;
    }

    @NonNull
    @Override
    public MyDataAdapter.DataViewHolder onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {
        View v = LayoutInflater.from(ct).inflate(R.layout.row_design, parent, false);
        return new DataViewHolder(v);
    }

    @Override
    public void onBindViewHolder(@NonNull MyDataAdapter.DataViewHolder holder, int position) {
        final Student list = students.get(position);
        holder.rroll.setText(list.getRollNumber());
        holder.rname.setText(list.getName());
        holder.rmobile.setText(list.getMobileNUmber());
        holder.rmail.setText(list.getMailID());

        holder.delete.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                MainActivity.viewModel.delete(list);
            }
        });
    }

    @Override
    public int getItemCount() {
        return students.size();
    }

    public class DataViewHolder extends RecyclerView.ViewHolder {

        TextView rname, rmail, rmobile, rroll;
        ImageView delete;

        public DataViewHolder(@NonNull View itemView) {
            super(itemView);
            rname = itemView.findViewById(R.id.readname);
            rmail = itemView.findViewById(R.id.readMailid);
            rmobile = itemView.findViewById(R.id.readmobile);
            rroll = itemView.findViewById(R.id.readroll);
            delete = itemView.findViewById(R.id.delete);
        }
    }
}
```
