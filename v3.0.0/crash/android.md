# Android Installation

## Add the dependency

Add the Firebase Cloud Crash dependancy to `android/app/build.gradle`:

```
dependencies {
  ...
  compile "com.google.firebase:firebase-crash:{{ android.firebase.version }}"
}
```

## Install the RNFirebase Crash package

Add the `RNFirebaseCrashPackage` to your `android/app/src/main/java/com/[app name]/MainApplication.java`:

```java
...
import io.invertase.firebase.RNFirebasePackage;
import io.invertase.firebase.crash.RNFirebaseCrashPackage; // <-- Add this line

public class MainApplication extends Application implements ReactApplication {
    // ...

    @Override
    protected List<ReactPackage> getPackages() {
      return Arrays.<ReactPackage>asList(
          new MainReactPackage(),
          new RNFirebasePackage(),
          new RNFirebaseCrashPackage() // <-- Add this line
      );
    }
  };
  // ...
}
```
