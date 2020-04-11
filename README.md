# FirebaseAppDistribution-GithubAction

This Action is to Upload the Apk to Firebase App Disturbution

Reference Documents

https://firebase.google.com/docs/app-distribution/android/distribute-cli

## Required Paramaters


### `App ID`
**Required**: Your app's Firebase App ID. You can find the App ID in the Firebase console, on the General Settings page.

### `Token`
**Required**:	A refresh token that's printed when you authenticate your CI environment with the Firebase CLI (read Use the CLI with CI systems for more information).

### `File`
**Required** Apk to upload

### `groups`
Distribution groups

### `releaseNotes`
Release notes visible on release page.
 
### `releaseNotesFile`
Specify the release note path to a plain text file.

### `debug`
Flag that can be included to print verbose log output. Default value is `false`

## Example using Firebase Tool 

```firebase appdistribution:distribute test.apk  \
    --app 1:1234567890:android:0a1b2c3d4e5f67890  \
    --release-notes "Bug fixes and improvements" --testers-file testers.txt
```

Now i going to achieve same using action

## Sample


```
name: Build Debug APK & Upload to Firebase App Distribution 

on:
  push:
    branches: [ master ]

jobs:
  apk:
    name: Upload APk To FireBase App Disturbution
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v1
    - name: set up JDK 1.8
      uses: actions/setup-java@v1
      with:
        java-version: 1.8
    - name: Build a Debug Apk
      run: bash ./gradlew assembleDebug --stacktrace
    - name: upload artifact to Firebase App Distribution
      uses: manishkummar21/FirebaseAppDistribution-GithubAction@master
      with:
        appId: ${{secrets.FIREBASE_APP_ID}}
        token: ${{secrets.FIREBASE_TOKEN}}
        groups: QA
        file: app/build/outputs/apk/debug/app-debug.apk     
```

### Note:- Next Research is on How to Upload the Android App Bundle 
