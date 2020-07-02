# Facebook Sign-In Authentication

we will talk about the most trending authentication method of Firebase, i.e., Facebook. Facebook sign-in authentication is quite typical to implement.
The users can authenticate with Firebase using their Facebook accounts by integrating Facebook logging into our application.

So let's see the steps to implement Facebook sign-in authentication one by one.

**Step 1:**
In the first step, we will create an Android and Firebase project, and then we will add our Firebase project with our application. Also, add SHA-1 and SHA-256 keys in the Firebase console. After that, add all the required dependencies, i.e., firebase-core, firebase-auth, and plugin in 'app.build.gradle' file and classpath in 'build.gradle' file.

We will also add the Facebook login dependency in the 'app.build.gradle' file'.

![f1](https://user-images.githubusercontent.com/51777024/85914350-8bc91500-b85a-11ea-9364-0578c1588912.png)

**Step 2:**

In the next step, we have to create an application in the 'Facebook for developer' website. For creating a request, we should have a Facebook account. Login with the Facebook account. Then, go to the Facebook developer site with the help of the following link:

https://developers.facebook.com/

![f2](https://user-images.githubusercontent.com/51777024/85914353-91265f80-b85a-11ea-947e-66c0ebb56ce1.png)

Once our developer account is logged in, we will click on Docs to move on to the document page.

![f3](https://user-images.githubusercontent.com/51777024/85914356-95eb1380-b85a-11ea-9791-b3bb8b2ac0d5.png)

**Step 3:**

In the document page, we will scroll down and click on the Facebook login. And from the Facebook login page, we will select Android to move an android page from there, we will select an app or create a new app.

![f4](https://user-images.githubusercontent.com/51777024/85914360-9b485e00-b85a-11ea-8f36-b0f9cf56e781.png)

![f5](https://user-images.githubusercontent.com/51777024/85914364-9f747b80-b85a-11ea-9e46-3ef82cb6ddc9.png)

If we are not a developer, then we have to register as a developer by clicking on Register.

![f6](https://user-images.githubusercontent.com/51777024/85914366-a56a5c80-b85a-11ea-9ac1-8a3fc13b03f5.png)

Click on next to register as a Facebook developer.

![f7](https://user-images.githubusercontent.com/51777024/85914368-a8fde380-b85a-11ea-8bc9-6e40bf48e411.png)

After clicking on the next, a new screen will be visible from where select the developer option.

![f8](https://user-images.githubusercontent.com/51777024/85914370-ac916a80-b85a-11ea-80cb-41b11c876aa4.png)

After selecting developer, the welcome page will be opened.

![f9](https://user-images.githubusercontent.com/51777024/85914374-b1561e80-b85a-11ea-9892-89e4d13e2a70.png)

From the welcome page, select Create First App and give it a name for display and contact email and click on Create App ID.

![f10](https://user-images.githubusercontent.com/51777024/85914377-b4510f00-b85a-11ea-8448-f0e88a05bc9e.png)

Perform a security check.

![f11](https://user-images.githubusercontent.com/51777024/85914381-b7e49600-b85a-11ea-87e1-34b77d80e496.png)

![f12](https://user-images.githubusercontent.com/51777024/85914384-badf8680-b85a-11ea-94e2-339dfa4b31a6.png)

Now, go to Home->Doc->facebook login->android and select the app which we have created before and copied the App ID.

![f13](https://user-images.githubusercontent.com/51777024/85914386-bf0ba400-b85a-11ea-9247-0acd7e2cbaac.png)


**Step 4:**

In the next step, we will move to the 'string.xml' file of Android Studio and create two strings, i.e., facebook_app_id and fb_login_protocol_scheme. For facebook_app_id, we will paste the app id, which we have copied before, and for fb_login_protocol_scheme, we will add prefix FB in our app_id and use it as a protocol string.

![f14](https://user-images.githubusercontent.com/51777024/85914387-c29f2b00-b85a-11ea-9219-32ab5fcbeae3.png)

**Step 5:**

We also need to add permission for the Internet to our Android Manifest file.

![f15](https://user-images.githubusercontent.com/51777024/85914388-c59a1b80-b85a-11ea-8d5f-dbd6ca6b48e4.png)

**Step 6:**

In the next step, we will add the Metadata. For this, we will go to the Facebook developer site and copy the code of step 5.

![f16](https://user-images.githubusercontent.com/51777024/85914389-c92da280-b85a-11ea-8ffd-c1b7036c3441.png)

After copying the code, we will paste it in Manifest files after the MainActivity code.

![f17](https://user-images.githubusercontent.com/51777024/85914392-cc289300-b85a-11ea-8314-d988d7d391ea.png)

**Step 7:**

Now, we will associate our package name and default class with our app. So we will add the package name and default activity class name in the developer site.

![f18](https://user-images.githubusercontent.com/51777024/85914395-ce8aed00-b85a-11ea-8d20-3f1fbabc2d83.png)

**Step 8:**

In the next step, we will add the Development Key Hashes for our app. For this, we need openssl open library. If we don't have this library, then we first have to download the openssl library. And after that we will execute the following command in the command prompt:

![f19](https://user-images.githubusercontent.com/51777024/85914398-d0ed4700-b85a-11ea-985a-a79f9aaac4d6.png)

We will copy this key and paste it in the developer site's Key Hashes

![f20](https://user-images.githubusercontent.com/51777024/85914400-d3e83780-b85a-11ea-8660-c5952970713a.png)

**Step 9:**

In the next step, we have to enable single sign-on for our app in facebook developer sites.

![f21](https://user-images.githubusercontent.com/51777024/85914404-d77bbe80-b85a-11ea-82a0-f83afaf2cfbc.png)

**Step 10:**

In the next step, we will go to the basic setting of our app in the facebook developer site. And from here, we have to copy the App Secret that will be used in Firebase console.

![f22](https://user-images.githubusercontent.com/51777024/85914405-d9de1880-b85a-11ea-8c7f-c338266f2d52.png)

**Step 11:**

The App Secret, which we have copied from the Facebook developer site, will be pasted in the firebase console. When we enable the Facebook sign-in method, it will ask for the App ID and App Secret and provide OAuth redirect URL, which will be added to our app on the Facebook developer site.

![f23](https://user-images.githubusercontent.com/51777024/85914406-dcd90900-b85a-11ea-990b-c0914e432c93.png)

Now, we will go to the Facebook setting page. Here, we will add the OAuth redirect URL to Facebook login settings.

![f24](https://user-images.githubusercontent.com/51777024/85914408-df3b6300-b85a-11ea-9624-30357ce75f42.png)

**Step 12:**

In the next step, we will create a Facebook login button from the SDK. It is a UI element that wraps functionality available in the login manager.

![f25](https://user-images.githubusercontent.com/51777024/85914409-e2365380-b85a-11ea-8798-03b9eb915fec.png)

**Step 13:**

In the next step, we will modify our MainActivity.java file to perform the authentication using Facebook in the following way:

```
public class MainActivity extends AppCompatActivity {  
  
    private static final String TAG = "FacebookLogin";  
    private static final int RC_SIGN_IN = 12345;  
  
    private CallbackManager mCallbackManager;  
  
    private FirebaseAuth mAuth;  
  
    @Override  
    protected void onCreate(Bundle savedInstanceState) {  
        super.onCreate(savedInstanceState);  
        setContentView(R.layout.activity_main);  
  
        // Initialize Firebase Auth  
        mAuth = FirebaseAuth.getInstance();  
  
        // Initialize Facebook Login button  
        mCallbackManager = CallbackManager.Factory.create();  
  
        LoginButton loginButton = findViewById(R.id.login_button);  
  
        loginButton.setReadPermissions("email", "public_profile");  
        loginButton.registerCallback(mCallbackManager, new FacebookCallback<LoginResult>() {  
            @Override  
            public void onSuccess(LoginResult loginResult) {  
                Log.d(TAG, "facebook:onSuccess:" + loginResult);  
                handleFacebookAccessToken(loginResult.getAccessToken());  
            }  
  
            @Override  
            public void onCancel() {  
                Log.d(TAG, "facebook:onCancel");  
            }  
  
            @Override  
            public void onError(FacebookException error) {  
  
            }  
  
        });  
    }  
  
    @Override  
    public void onStart() {  
        super.onStart();  
  
        // Checking if the user is signed in (non-null) and update UI accordingly.  
        FirebaseUser currentUser = mAuth.getCurrentUser();  
  
        if (currentUser != null) {  
            Log.d(TAG, "Currently Signed in: " + currentUser.getEmail());  
            Toast.makeText(MainActivity.this, "Currently Logged in: " + currentUser.getEmail(), Toast.LENGTH_LONG).show();  
        }  
    }  
    @Override  
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {  
        super.onActivityResult(requestCode, resultCode, data);  
  
        // The activity result pass back to the Facebook SDK  
        mCallbackManager.onActivityResult(requestCode, resultCode, data);  
    }  
  
    private void handleFacebookAccessToken(AccessToken token) {  
        Log.d(TAG, "handleFacebookAccessToken:" + token);  
  
        AuthCredential credential = FacebookAuthProvider.getCredential(token.getToken());  
  
        mAuth.signInWithCredential(credential)  
                .addOnCompleteListener(this, new OnCompleteListener<AuthResult>() {  
                    @Override  
                    public void onComplete(@NonNull Task<AuthResult> task) {  
                        if (task.isSuccessful()) {  
                            // Sign in success, UI will update with the signed-in user's information  
                            Log.d(TAG, "signInWithCredential:success");  
                            FirebaseUser user = mAuth.getCurrentUser();  
                            Toast.makeText(MainActivity.this, "Authentication Succeeded.", Toast.LENGTH_SHORT).show();  
                        } else {  
                            // If sign-in fails, a message will display to the user.  
                            Log.w(TAG, "signInWithCredential:failure", task.getException());  
                            Toast.makeText(MainActivity.this, "Authentication failed.", Toast.LENGTH_SHORT).show();  
                        }  
                    }  
                });  
    }  
}  
```
**Output:**

![f26](https://user-images.githubusercontent.com/51777024/85914411-e5c9da80-b85a-11ea-9c8b-8bc80de000ac.png)

![f28](https://user-images.githubusercontent.com/51777024/85914810-71456a80-b85f-11ea-9bf2-17b9b0eeb0e0.png)

![f27](https://user-images.githubusercontent.com/51777024/85914415-f712e700-b85a-11ea-956b-91133e7edf64.png)

