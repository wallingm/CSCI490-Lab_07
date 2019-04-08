# CSCI490-Lab_07

This lab demostrates Firebase services from Google. In order to bring in these powerful features in the finished app, you will need to create a project using the Firebase Console. Instructions to do this are next. If you don’t have a Google account yet, you can create one [here](https://accounts.google.com/signup/v2/webcreateaccount?flowName=GlifWebSignIn&flowEntry=SignUp). 


## Create Project in Firebase Console ##
* Start by navigating to the [Firebase Console](https://console.firebase.google.com/) webpage.
* Select "Add PROJECT" and name your project. Fill in the name and agree to the terms. Click 'Create Project'.
* When the project is ready, click 'Continue'.

## Get started by adding Firebase to your app ##
* Click the Andoid icon to add an Android app to the Firebase project
* Add your package name for the app. This can be found in the Manifest file.
* Click 'Register App'.
* You’ll need to add the debug signing certificate too because you’ll implement Google Sign-In for authentication in FriendlyChat. The SHA-1 is a type of hash representation for the debug keystore, which you can get with the keytool command line tool. Which is a long way of saying, the debug keystore is a bunch of letters and numbers, which you should keep secret, that identifies your computer.

On Windows, open the Command Prompt program. You can do this by going to the Start menu
````
keytool -exportcert -list -v \
-alias androiddebugkey -keystore %USERPROFILE%\.android\debug.keystore
````
On Mac/Linux, open the Terminal and paste
````
keytool -exportcert -list -v \
-alias androiddebugkey -keystore ~/.android/debug.keystore
````
* Copy and paste the 'SHA1' string and paste into the Firebase Console certificate section. 
* Download the google-services.json file and add to the app/ directory of your project.
* Add the Firebase SDK to your project by following the directions from the Firebase Console.
* Make sure you 'Sync Now'

## Adding Firebase Realtime Database to your app ##
* Firebase Realtime Database must be added to your app. Add ***implementation 'com.google.firebase:firebase-database:16.0.1'*** to your app/build.gradle file in the ***dependencies*** section.
* More information can be found [here](https://firebase.google.com/docs/android/setup), however I have not had much luck in using this page. Version numbers seem to be off and never compatible with what I am doing. 

## Use Firebase Database ##
* Add the Database references to you ***MainActivity.java***
````
private FirebaseDatabase mFirebaseDatabase;
private DatabaseReference mMessagesDatabaseReference;
````
The FirebaseDatabase object will be a reference to your entire FirebaseDatabase and the DatabaseReference object will be a reference to the ***messages*** collection. 

* Add the following code in your ***onCreate()*** method:
````
mFirebaseDatabase = FirebaseDatabase.getInstance();
mMessagesDatabaseReference = mFirebaseDatabase.getReference().child("messages");
````
* Ensure there is an OnClickListener attached to the button
````
// Send button sends a message and clears the EditText
mSendButton.setOnClickListener(new View.OnClickListener() {
   @Override
   public void onClick(View view) {
       // TODO: Send messages on click


       // Clear input box
       mMessageEditText.setText("");
   }
});
````
Within the onClick method, let’s create a FriendlyMessage object for the message that the user typed in. The FriendlyMessage object has three instance variables: A String for the user’s name, A String for the text of the message A String for the URL of the photo if it’s a photo message.

In this case, we’re only sending text messages for now (we will implement photo-messaging later), so we’ll create a FriendlyMessage object with all the fields except for photoUrl, which will be null.
Set up the ChildEventListener
````
private void attachDatabaseReadListener() {
        if(mChildEventListner == null) {
            mChildEventListner = new ChildEventListener() {
                @Override
                public void onChildAdded(DataSnapshot dataSnapshot, String s) {
                  

                }

                @Override
                public void onChildChanged(DataSnapshot dataSnapshot, String s) {

                }

                @Override
                public void onChildRemoved(DataSnapshot dataSnapshot) {
            

                }

                @Override
                public void onChildMoved(DataSnapshot dataSnapshot, String s) {

                }

                @Override
                public void onCancelled(DatabaseError databaseError) {

                }
            };

            mMessagesDatabaseReference.addChildEventListener(mChildEventListner);
        }
    }
````
````
private void detachDatabaseReadListener() {
    if(mChildEventListner != null) {
        mMessagesDatabaseReference.removeEventListener(mChildEventListner);
        mChildEventListner = null;

    }
}
````
    
