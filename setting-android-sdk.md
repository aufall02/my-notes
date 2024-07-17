## set Android SDK Without

- [download](https://dl.google.com/android/repository/commandlinetools-win-11076708_latest.zip)
- setup
    - ekstrak file hasil download
    - buat folder ```Android/cmdline-tools/latest``` di disk C
    - paste kan isi dari hasil ekstrak ke dalam folder ```Android/cmdline-tools/latest```
    - buka commandpromt pada folder ```AAndroid/cmdline-tools/latest/bin```
    - masukkan perintah ```sdkmanager "platform-tools" "platforms;android-33"``` 
    - masukkan perintah ```sdkmanager "build-tools;34.0.0"```
    - set up env variable
      - masukkan ```C:\Android\platforms``` pada path user-variable
      - tambahan varibale ```ANDROID_HOME``` dengan nilai ```C:\Android``` 


## Referensi
- [How to Install Android Command Line Tools without Android Studio - DM Inspires](https://www.youtube.com/watch?v=EuEPhYAb-bU)