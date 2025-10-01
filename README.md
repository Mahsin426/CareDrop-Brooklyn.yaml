steps:
  - name: Checkout repository
    uses: actions/checkout@v3

  - name: Setup Node.js
    uses: actions/setup-node@v3
    with:
      node-version: 18

  - name: Install dependencies
    run: |
      # Assuming this is a React Native project, install JS dependencies
      npm install --legacy-peer-deps

  - name: Setup JDK 11
    uses: actions/setup-java@v3
    with:
      distribution: 'temurin'
      java-version: '11'

  - name: Setup Android SDK
    uses: android-actions/setup-android@v3

  - name: Grant execution permission to gradlew
    run: chmod +x android/gradlew

  - name: Build release APK
    run: |
      # Change directory to the Android project and execute the Gradle wrapper
      cd android
      ./gradlew assembleRelease

  - name: Upload APK artifact
    uses: actions/upload-artifact@v3
    with:
      name: CareDrop-Brooklyn-APK
      path: android/app/build/outputs/apk/release/app-release.apk
.yaml
  name--CareDropBrooklyn-APK    
