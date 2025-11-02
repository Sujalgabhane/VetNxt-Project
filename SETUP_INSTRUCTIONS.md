# LivHealth HMIS - Setup Instructions

## Quick Start Guide

### 1. Open Project in Android Studio

1. Launch Android Studio (version Hedgehog or newer recommended)
2. File → Open → Select the `LivHealth` folder
3. Wait for Gradle sync to complete (may take a few minutes on first run)

### 2. Configure Firebase (Optional but Recommended)

If you plan to use Firebase for backend sync:

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Create a new project or select existing
3. Add Android app:
   - Package name: `com.yourorg.livhealth`
   - App nickname: LivHealth HMIS
   - Download `google-services.json`
4. Replace `app/google-services.json` with the downloaded file
5. Sync Gradle again

**Note:** If you don't use Firebase, the app will still work with local database only. Background sync will need a custom implementation.

### 3. Sync Gradle Dependencies

- Click "Sync Now" if Android Studio prompts you
- Or: File → Sync Project with Gradle Files
- Wait for all dependencies to download

### 4. Run the App

#### On Emulator:
1. Tools → Device Manager → Create Device
2. Choose a device (e.g., Pixel 5)
3. Select system image (API 21 or higher)
4. Run → Run 'app' (or press Shift+F10)

#### On Physical Device:
1. Enable Developer Options:
   - Settings → About Phone → Tap "Build Number" 7 times
2. Enable USB Debugging:
   - Settings → Developer Options → USB Debugging
3. Connect device via USB
4. Run → Run 'app' → Select your device

**Important:** NFC features require a physical device. Most emulators don't support NFC.

### 5. Testing Features

#### Test QR Scanning:
1. Launch app
2. Tap "Scan QR / NFC"
3. Grant camera permission
4. Point camera at a QR code
5. QR value should be detected automatically

#### Test NFC (Physical Device Only):
1. Ensure NFC is enabled on device
2. Launch app
3. Tap an NFC tag (NDEF format with text/plain)
4. App should detect and process the tag

#### Test Add Animal:
1. From home screen, tap "Add Animal"
2. Fill in:
   - Animal ID (required, e.g., "MH-001")
   - Owner Name (required)
   - Breed (optional)
   - Village (optional)
3. Tap "Save Animal"

#### Test Offline Sync:
1. Add health records while offline (Airplane mode)
2. Disable Airplane mode
3. WorkManager will sync records automatically (every hour)
4. Check Logcat for sync logs: `adb logcat | grep SyncWorker`

## Project Structure

```
LivHealth/
├── app/
│   ├── src/
│   │   └── main/
│   │       ├── java/com/yourorg/livhealth/
│   │       │   ├── data/              # Room database, entities, DAOs, Repository
│   │       │   ├── viewmodel/         # ViewModels (ScanViewModel, HomeViewModel)
│   │       │   ├── ui/
│   │       │   │   ├── screens/        # Compose screens
│   │       │   │   └── theme/          # Material theme
│   │       │   ├── work/               # WorkManager (SyncWorker)
│   │       │   └── MainActivity.kt     # Main activity with NFC handling
│   │       ├── res/                    # Resources (strings, themes)
│   │       └── AndroidManifest.xml
│   ├── build.gradle                   # App-level dependencies
│   └── google-services.json           # Firebase config (replace with yours)
├── build.gradle                       # Project-level build config
├── settings.gradle                    # Gradle settings
└── gradle.properties                  # Gradle properties

```

## Key Features Implemented

✅ Room Database for local storage  
✅ QR Code scanning with CameraX + ML Kit  
✅ NFC tag reading  
✅ Jetpack Compose UI  
✅ WorkManager for background sync  
✅ Navigation with Compose Navigation  
✅ Runtime permission handling  
✅ ViewModel for state management  

## Build Signed APK for Distribution

1. Build → Generate Signed Bundle / APK
2. Choose APK
3. Create new keystore:
   - Key store path: choose location
   - Password: set secure password
   - Key alias: create alias
   - Key password: set password
   - Validity: 25 years
4. Click OK → Finish
5. Signed APK will be at: `app/release/app-release.apk`

## Troubleshooting

### Gradle Sync Fails
- Check internet connection
- File → Invalidate Caches → Invalidate and Restart
- Check `gradle.properties` for proxy settings if behind firewall

### Camera Permission Denied
- Go to Settings → Apps → LivHealth HMIS → Permissions
- Enable Camera permission manually

### NFC Not Working
- Ensure NFC is enabled in device settings
- Test with a known working NFC tag
- Check Logcat for NFC-related errors
- Some devices require NFC to be enabled in settings separately

### ML Kit Not Detecting QR Codes
- Ensure good lighting
- QR code should be at least 4-6 cm
- Try different distances from camera
- Check Logcat: `adb logcat | grep CameraPreview`

### Database Issues
- Uninstall and reinstall app to reset database
- Check Logcat for Room database errors

## Next Steps

1. **Customize Theme**: Edit `ui/theme/Theme.kt`
2. **Implement Backend Sync**: Replace placeholder in `SyncWorker.kt` with actual API calls
3. **Add More Features**: 
   - Animal search
   - Health record history view
   - Export reports
   - QR code generation for new animals

## Support

For issues or questions, check:
- Android Developer Documentation
- Jetpack Compose Guides
- Room Database Guide
- CameraX Documentation

