# Android Installation

First ensure you have followed the [initial setup guide](version /installation/initial-setup).

## Add the dependency

Add the Firebase Performance Monitoring dependancy to `android/app/build.gradle`:

```groovy
dependencies {
  // ...
  compile "com.google.firebase:firebase-perf:{{ android.firebase.version }}"
}
```

Performance Monitoring also requires the Firebase Plugins dependency. In your projects `android/build.gradle` file, add the plugin to your dependencies:

```groovy
dependencies {
  // ...
  classpath 'com.google.firebase:firebase-plugins:{{ android.firebase.plugins }}'
}
```

At the top of your `android/app/build.gradle` file, below other plugins, apply the `firebase-perf` plugin:

```groovy
apply plugin: "com.android.application"
apply plugin: "com.google.firebase.firebase-perf"
```

## Install the RNFirebase Performance package

Add the `RNFirebasePerformancePackage` to your `android/app/src/main/java/com/[app name]/MainApplication.java`:

```java
// ...
import io.invertase.firebase.RNFirebasePackage;
import io.invertase.firebase.perf.RNFirebasePerformancePackage; // <-- Add this line

public class MainApplication extends Application implements ReactApplication {
    // ...

    @Override
    protected List<ReactPackage> getPackages() {
      return Arrays.<ReactPackage>asList(
          new MainReactPackage(),
          new RNFirebasePackage(),
          new RNFirebasePerformancePackage() // <-- Add this line
      );
    }
  };
  // ...
}
```
