# Setting Up Background Location in Unity with LAN LiveLocation Plugin

This guide walks you through setting up background location functionality in Unity using the LAN LiveLocation plugin. Follow the steps below to ensure a smooth integration.

---

## Supported Platforms

- **Android OS**: Tested on Android 10 and Android 14 devices.
- **iOS**: Coming soon.

---

## Requirements and Installation

### Step 1: Install External Dependency Manager for Unity

To manage dependencies, you need to install the External Dependency Manager for Unity:

- Follow the [manual installation guide](https://openupm.com/packages/com.google.external-dependency-manager/#modal-manualinstallation).
- Alternatively, download and import the [latest custom package](https://github.com/googlesamples/unity-jar-resolver/blob/master/external-dependency-manager-latest.unitypackage).

### Step 2: Install the Live Location Plugin

Add the Live Location plugin to your Unity project:

1. Open the **Package Manager** window.
2. Click the **Add** button in the toolbar.
3. Select **Add package from git URL**.
4. Paste the following URL: `https://github.com/krlan2789/Unity-LAN-LiveLocation-Plugin.git`.

<img class="use-github-assets" src="./Screenshot/Add_package_from_git_url.png" height="auto" width="640px" />

### Step 3: Set Minimum API Level

Ensure the minimum API level is set to **API Level 26**.

<img class="use-github-assets" src="./Screenshot/Min_Android_API_Level.png" height="auto" width="640px" />

### Step 4: Verify Build Settings

Check and configure the required build settings.

<img class="use-github-assets" src="./Screenshot/Build_Settings.png" height="auto" width="640px" />

### Step 5: Update AndroidManifest.xml

Add the following permissions to `Assets/Plugins/Android/AndroidManifest.xml`:

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android" package="com.LAN.BackgroundLocation" xmlns:tools="http://schemas.android.com/tools">

     <!-- Required permissions -->
     <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
     <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
     <uses-permission android:name="android.permission.ACCESS_BACKGROUND_LOCATION" />
     <uses-permission android:name="android.permission.FOREGROUND_SERVICE" />
     <uses-permission android:name="android.permission.FOREGROUND_SERVICE_LOCATION" android:minSdkVersion="29" />
     <!-- Optional permissions -->
     <uses-permission android:name="android.permission.REQUEST_IGNORE_BATTERY_OPTIMIZATIONS" />

     <application>
          <activity android:name="com.unity3d.player.UnityPlayerActivity" android:theme="@style/UnityThemeSelector">
          ...
     </application>
</manifest>
```

### Step 6: Update launcherTemplate.gradle

Insert the following script into `Assets\Plugins\Android\launcherTemplate.gradle`:

```gradle
android {
     ...
     packagingOptions {
          pickFirst('META-INF/okio.kotlin_module')
          pickFirst('META-INF/kotlinx_coroutines_core.version')
     }
}
```

### Step 7: Update mainTemplate.gradle

Insert the following script into `Assets\Plugins\Android\mainTemplate.gradle`:

```gradle
android {
     ...
     packagingOptions {
          pickFirst('META-INF/okio.kotlin_module')
          pickFirst('META-INF/kotlinx_coroutines_core.version')
     }
}
```

### Step 8: Update gradleTemplate.properties

Insert the following script into `Assets\Plugins\Android\gradleTemplate.properties`:

```properties
android.enableJetifier=true
android.suppressUnsupportedCompileSdk=34
```

---

## Common Errors and Troubleshooting

### `Custom Gradle Properties Template` :

<img class="use-github-assets" src="./Screenshot/Error_gradleproperties_unchecked_popup.png" height="auto" width="640px" />

<img class="use-github-assets" src="./Screenshot/Error_gradleproperties_unchecked.png" height="auto" width="640px" />

### `Custom Launcher Gradle` and `Custom Main Gradle` :

<img class="use-github-assets" src="./Screenshot/Error_manifestgradle_unchecked_popup.png" height="auto" width="640px" />

<img class="use-github-assets" src="./Screenshot/Error_manifestgradle_unchecked.png" height="auto" width="640px" />

---

By following these steps, you can successfully integrate background location functionality into your Unity project using the LAN LiveLocation plugin. For further assistance, refer to the plugin's documentation or community forums.
