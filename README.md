# Ayush
Hi mai Jarvis apk assistant agent hu

name: Build JARVIS APK

on:
  workflow_dispatch:
  push:
    paths:
      - 'JARVIS_Android_Project.zip'
      - '.github/workflows/build.yml'

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: '17'

      - uses: gradle/actions/setup-gradle@v4
        with:
          gradle-version: '8.9'

      - name: Extract project
        run: unzip JARVIS_Android_Project.zip

      - name: Build APK
        working-directory: JARVIS_Android_Project
        run: gradle assembleDebug

      - uses: actions/upload-artifact@v4
        with:
          name: JARVIS-APK
          path: JARVIS_Android_Project/app/build/outputs/apk/debug/app-debug.apk
