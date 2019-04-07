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

