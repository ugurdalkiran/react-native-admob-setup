# React Native Google AdMob Setup

[sbugert/react-native-admob](https://github.com/sbugert/react-native-admob) this plugin was used.

In the React Native **0.57.X** versions, the unity was prepared through the project that was tested and worked.

**WARNING: react-native link** Do not automatic do manual.

# Setup

We will update 6 files in total.

```
1. android/settings.gradle
2. android/build.gradle
3. android/app/build.gradle
4. android/app/src/main/AndroidManifest.xml
5. android/app/src/main/java/com/PROJECT_NAME/MainApplication.java
6. android/app/src/main/java/com/PROJECT_NAME/MainActivity.java
```

## 1. android/settings.gradle

```gradle
include ':react-native-admob'
project(':react-native-admob').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-admob/android')
```

## 2. android/build.gradle

```gradle
allprojects {
  repositories {
    mavenLocal()
    google()
    jcenter()
    maven {
      // All of React Native (JS, Obj-C sources, Android binaries) is installed from npm
      url "https://maven.google.com" // IMPORTANT!!!
      url "$rootDir/../node_modules/react-native/android"
    }
  }
}
```

## 3. android/app/build.gradle

```gradle
dependencies {
  implementation( project(':react-native-admob') ){
    exclude group: "com.google.android.gms"
  }
  implementation "com.google.android.gms:play-services-ads:17.1.1"
}
```

## 4. android/app/src/main/AndroidManifest.xml

```xml
<application>

  <meta-data
    android:name="com.google.android.gms.ads.APPLICATION_ID"
    android:value="GOOGLE_ADMOB_APP_ID" />

</application>
```

## 5. android/app/src/main/java/com/PROJECT_NAME/MainApplication.java

```java
import com.sbugert.rnadmob.RNAdMobPackage;

@Override
protected List<ReactPackage> getPackages() {
  return Arrays.<ReactPackage>asList(
    ...
    new RNAdMobPackage(),
    ...
  );
}
```

## 5. android/app/src/main/java/com/PROJECT_NAME/MainActivity.java

```java
import android.os.Bundle;
import com.google.android.gms.ads.MobileAds;

@Override
protected void onCreate(Bundle savedInstanceState) {
  super.onCreate(savedInstanceState);
  MobileAds.initialize(this, "GOOGLE_ADMOB_APP_ID");
}
```

The end. :)
