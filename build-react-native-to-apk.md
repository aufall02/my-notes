## Build react native to apk for realese version

konfig file sebelum melakukan build

- Generating an upload key
  ```bash
  keytool -genkeypair -v -storetype PKCS12 -keystore my-upload-key.keystore -alias my-key-alias -keyalg RSA -keysize 2048 -validity 10000
  ```
- pindah file `my-upload-key.keystore` ke dalam folder android/app di project.
- edit file `android/gradle.properties` di project.
   ```bash
   MYAPP_UPLOAD_STORE_FILE=my-upload-key.keystore
   MYAPP_UPLOAD_KEY_ALIAS=my-key-alias
   MYAPP_UPLOAD_STORE_PASSWORD=*****
   MYAPP_UPLOAD_KEY_PASSWORD=*****
   ```
- edit file `android/app/build.gradle`
  ```bash
    android {
        signingConfigs {
            release {
                if (project.hasProperty('MYAPP_UPLOAD_STORE_FILE')) {
                    storeFile file(MYAPP_UPLOAD_STORE_FILE)
                    storePassword MYAPP_UPLOAD_STORE_PASSWORD
                    keyAlias MYAPP_UPLOAD_KEY_ALIAS
                    keyPassword MYAPP_UPLOAD_KEY_PASSWORD
                }
                
            }
        }
        buildTypes {
            release {
                signingConfig signingConfigs.release
            }
        }
    }
  ```
- agar size file menjadi lebih kecil edit file `android/app/build.gradle:`
  ```bash
  def enableProguardInReleaseBuilds = true
  ```


Run Apk release mode
 ```bash
 npx react-native build-android --mode=release
 ```
Build with gradle
```bash
cd android && ./gradlew assembleRelease
```

## Referensi
* [React Native Generate APK - Anshul Borawake](https://medium.com/geekculture/react-native-generate-apk-debug-and-release-apk-4e9981a2ea51)
* [React Native build Apk - Docs react native](https://reactnative.dev/docs/signed-apk-android)