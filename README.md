# Example App of Google Auth Signin using React Native and Firebase

- Generate a fresh React Native app (I use a Typescript template, you can use any template or no template at all),
  I highly recommand to choose a random app name for a reason I will explain in a later step:

```bash
npx react-native init App_972035 --template react-native-template-typescript
```

- Install required packages:

  ```bash
  yarn add @react-native-firebase/app @react-native-firebase/auth @react-native-google-signin/google-signin
  ``

  ```

- Modify some files:

  - in `./android/build.gradle` add:
    ```gradle
    buildscript {
      ext {
        // ...
        googlePlayServicesAuthVersion = "19.2.0"
      }
      dependencies {
        // ...
        classpath("com.google.gms:google-services:4.3.14")
        // ...
      }
    }
    ```
  - in `./android/app/build.gradle` add this:
    ```gradle
    apply plugin: "com.google.gms.google-services" // sould be at the end of the file
    ```

- Retrieve and note the _Android package name_, you can find it in file `./android/app/src/main/AndroidManifest.xml`
  in the `manifest` tag as value of the `package=` property, mine is for example `com.app_972035`
- Retrieve the `SHA1` and `SHA256` _certeficate fingerprints_ by runing the following commmand:
  ```bash
  cd android && ./gradlew signingReport
  ```
  Then in the section named `Variant: debugAndroidTest`, note the two values of `SHA1` and `SHA-256`, my `SHA1` is for example `5E:8F:16:06:2E:A3:CD:2C:4A:0D:54:78:76:BA:A6:F3:8C:AB:F6:25`, and it should be the same for you (and this can be problematic as I will explain later)
- Go to your [Firebase console](https://console.firebase.google.com/)
- Create a new project, name it `App-972035` for example (you can choose to not ativate Google Analytics, we don't need it)
- In this project, create an Android application by clicking on the Android icon
- Put the _Android package name_ you previously noted in the first field (Android Package Name)
- Put the `SHA1` _certeficate fingerprint_ in the last field (SHA-1 debuging certeficate fingerprint)
  > If you get an error `Oauth client already exists in a different project for package name com.package_name and certificate hash`,
  > it's probably that you didn't follow my recommendation of step 1. In fact, Google prevents that two apps with an OAuth 2.0 client
  > ID share the same package name and SHA-1 fingerprint at the same time (see [this answer](https://support.googles.ltd/firebase/answer/6401008?hl=en&ref_topic=6399725)).
  > So, for example, if you named your app `App`, it is highly likely that someone else somewhere did have the same brillant idea,
  > and did register an Android app on Firebase too. Thus, you can't register another app with the same name and the same fingerprint.
  > If you got this error, just repeat steps with another app name (following my advice... this time!)
- Download the configuration file (`google-services.json`), then put it inside the `./android/app/` folder
- Connect your android device
- Start the Metro server:
```bash
npx react-native start
```
- On another terminal, run the build
```bash
npx react-native run-android
```
