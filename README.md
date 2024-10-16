# AppAuth

_A simple and delightful way to integrate Firebase authentication into your Android apps!_

## Table of Contents
- [About AppAuth](#about-appauth)
- [Features](#features)
- [Installation](#installation)
- [How to Use](#how-to-use)
- [Technologies Used](#technologies-used)
- [Contributing](#contributing)
- [License](#license)

## About AppAuth

**AppAuth** is an Android library designed to make Firebase authentication integration smooth and straightforward. With built-in support for Google sign-in and more, AppAuth allows developers to easily implement authentication workflows with minimal effort.

### Why use AppAuth?
- Simplifies Firebase authentication setup in Android apps.
- Reduces boilerplate code for handling login workflows.
- Supports Google login with a few lines of code.
- Easily customizable for more authentication providers.

## Features
- 🔒 **Firebase Authentication**: Easily integrate Firebase authentication into your Android app.
- 👤 **Google Sign-In**: Support for Google login out of the box.
- 🛠️ **Dagger Hilt Support**: Integrate seamlessly with Dagger Hilt for dependency injection.
- ⚙️ **Minimal Setup**: Just a few lines to launch the login screen and handle authenticated users.

## Installation

To install `AppAuth`, follow these steps:

### Step 1: Update the `project-level build.gradle`

In the `build.gradle` of your root project, add these plugins:

```groovy
plugins {
    id("com.google.dagger.hilt.android") version "latest.version" apply false
    id("com.google.gms.google-services") version "latest.version" apply false
}

dependencies {
    classpath("com.google.gms:google-services:latest-version")
}
```
### Step 2: Update the app-level build.gradle

In your `app/build.gradle` file, apply the necessary plugins and add the required dependencies:

```groovy
plugins {
    id "kotlin-kapt"
    id "com.google.dagger.hilt.android"
    id "com.google.gms.google-services"
}

dependencies {
    // Dagger Hilt for dependency injection
    implementation("com.google.dagger:hilt-android:2.51.1")
    kapt("com.google.dagger:hilt-compiler:2.51.1")
}

```

Add the following block for Jetpack Compose support if using Compose:
```groovy
android {
    ...
    composeOptions {
        kotlinCompilerExtensionVersion = "1.5.0"
    }
}
```

### Step 3: Add `google-services.json` and enable google auth

Download the `google-services.json` file from the Firebase console:

1. Go to your Firebase project.
2. Click on the settings gear icon, then select **"Project Settings."**
3. Under **"Your apps,"** find the Android app and click **"Download google-services.json."**
4. Place the downloaded `google-services.json` file inside the `app/` directory of your Android project.

This file contains configuration details necessary for Firebase services to work correctly in your app. Make sure this file is included in your version control to allow other developers to build the project without issues.

5. In your strings.xml file (located in res/values/), add the web_client_id string for Google login:
In your strings.xml file (located in res/values/), add the web_client_id string for Google login:
```xml
<resources>
    <string name="web_client_id">YOUR_WEB_CLIENT_ID_HERE</string>
</resources>
```
Replace `YOUR_WEB_CLIENT_ID_HERE` with the actual Web Client ID from your Firebase console.


### How to use

To launch the login screen from your activity, use the following code:

```kotlin
val intent = Intent(this, AuthLibraryActivity::class.java)
startActivity(intent)
```

If you are using Jetpack Compose, you can launch the login screen like this:

```kotlin
val context = LocalContext.current
context.startActivity(Intent(context, AuthLibraryActivity::class.java))
```
This will take the user to the authentication screen provided by the AppAuth library, allowing them to log in using Firebase authentication.


To retrieve the currently authenticated user in your activity, use the following code snippet:

```kotlin
private val authenticationViewModel: AuthenticationViewModel by viewModels()

authenticationViewModel.getConnectedUser().observe(this, Observer { user ->
    // Handle the authenticated user
    if (user != null) {
        // User is logged in
        // Perform actions with the user object
    } else {
        // No user is logged in
    }
})
```

### Screenshot
<img src="https://github.com/user-attachments/assets/a207c85c-276c-470d-a873-4a47627d8106" width="180" />

<img src="https://github.com/user-attachments/assets/439c58ff-ea93-4994-8ceb-d6c1cddde34c" width="180" />
<img src="https://github.com/user-attachments/assets/5a93ae31-d199-4ebf-b8ac-eaadb04163e0" width="180" />
<img src="https://github.com/user-attachments/assets/7d0b4b35-5a67-4daf-ab34-bb079922f971" width="180" />


