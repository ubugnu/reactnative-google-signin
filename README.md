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
