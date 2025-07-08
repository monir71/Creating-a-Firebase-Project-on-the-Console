https://console.firebase.google.com

Get started by adding Firebase to your app

Add Firebase to your Android app

```
1
Register app

Android package name
com.example.northhunterfootball

App nickname (optional)
NH Football

Debug signing certificate SHA-1 (optional)
44:CE:E0:9B:21:98:51:39:DB:CD:8E:EA:55:8F:7F:25:3D:D3:D6:2A

Required for Dynamic Links, and Google Sign-In or phone number support in Auth. Edit SHA-1s in Settings.

2
Download and then add config file

3
Add Firebase SDK

4
Next steps

Go to Gradle->Tasks->Android->signingReport

If not found, try explicitly adding this block to your build.gradle.kts just to help force Gradle to recognize the Android plugin:

plugins {
    id("com.android.application")
    id("org.jetbrains.kotlin.android")
}

Replace the alias(...) lines only temporarily with the above. This will help rule out any alias issues from the libs.versions.toml.

2
Download and then add config file

Instructions for Android Studio below
|
UnityC++
Switch to the Project view in Android Studio to see
your project root directory.

Move your downloaded google-services.json file
into your module (app-level) root directory.

google-services.json
Project->App->(paste google-services.json)

3
Add Firebase SDK

Instructions for Gradle
|
UnityC++
tip:
Are you still using the buildscript syntax to manage plugins? Learn how to add Firebase plugins using that syntax.
To make the google-services.json config values accessible to Firebase SDKs, you need the Google services Gradle plugin.


Kotlin DSL (build.gradle.kts)

Groovy (build.gradle)
Add the plugin as a dependency to your project-level build.gradle.kts file:

Root-level (project-level) Gradle file (<project>/build.gradle.kts):
plugins {
  // ...

  // Add the dependency for the Google services Gradle plugin
  id("com.google.gms.google-services") version "4.4.3" apply false

}
Then, in your module (app-level) build.gradle.kts file, add both the google-services plugin and any Firebase SDKs that you want to use in your app:

Module (app-level) Gradle file (<project>/<app-module>/build.gradle.kts):
plugins {
  id("com.android.application")

  // Add the Google services Gradle plugin
  id("com.google.gms.google-services")

  ...
}

dependencies {
  // Import the Firebase BoM
  implementation(platform("com.google.firebase:firebase-bom:33.16.0"))


  // TODO: Add the dependencies for Firebase products you want to use
  // When using the BoM, don't specify versions in Firebase dependencies
  implementation("com.google.firebase:firebase-analytics")
  
	/* My observation here
		//analytics should have a version, so not abobe line but below:
		implementation("com.google.firebase:firebase-analytics:21.5.0")
	*/


  // Add the dependencies for any other desired Firebase products
  // https://firebase.google.com/docs/android/setup#available-libraries
}
By using the Firebase Android BoM, your app will always use compatible Firebase library versions. Learn more
After adding the plugin and the desired SDKs, sync your Android project with Gradle files.
```
