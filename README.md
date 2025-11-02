# LivHealth HMIS

Livestock Health Management Information System - An Android application for tracking animal health records using QR codes and NFC tags.

## Features

- **QR Code Scanning**: Scan QR codes using device camera with ML Kit
- **NFC Tag Reading**: Read animal IDs from NFC tags
- **Local Database**: Room database for offline-first operation
- **Background Sync**: Automatic sync of health records using WorkManager
- **Modern UI**: Built with Jetpack Compose

## Setup Instructions

1. **Open in Android Studio**
   - File → Open → Select this project folder
   - Wait for Gradle sync to complete

2. **Configure Firebase (Optional)**
   - Go to [Firebase Console](https://console.firebase.google.com/)
   - Create a new project
   - Add Android app with package name: `com.yourorg.livhealth`
   - Download `google-services.json` and replace the placeholder in `app/google-services.json`

3. **Sync Gradle**
   - Click "Sync Now" when prompted
   - Ensure all dependencies are downloaded

4. **Run the App**
   - Connect an Android device or start an emulator
   - Click Run → Run 'app'

## Testing

### QR Code Scanning
- Test with printed QR codes (4-6 cm recommended size)
- Ensure good lighting conditions
- Grant camera permission when prompted

### NFC Tag Reading
- Requires a physical Android device with NFC capability
- Most emulators don't support NFC
- Test with writable NFC tags (NDEF format)

### Offline Testing
- Enable Airplane mode
- Create health records
- Disable Airplane mode
- Check WorkManager logs for sync status

## Project Structure

```
app/src/main/java/com/yourorg/livhealth/
├── data/              # Room entities, DAOs, Database, Repository
├── viewmodel/         # ViewModels for UI state management
├── ui/
│   ├── screens/       # Compose screens (Home, Scan, Result, Add)
│   └── theme/         # Material theme configuration
├── work/              # WorkManager workers for background sync
└── MainActivity.kt    # Main activity with NFC handling
```

## Key Dependencies

- Jetpack Compose for UI
- Room for local database
- CameraX + ML Kit for QR scanning
- WorkManager for background sync
- Navigation Compose for navigation
- Accompanist Permissions for runtime permissions

## Build Signed APK

1. Build → Generate Signed Bundle / APK
2. Choose APK
3. Create new keystore or use existing
4. Build → Get signed APK from `app/release/`

## Notes

- Minimum SDK: API 21 (Android 5.0)
- Target SDK: API 34
- Language: Kotlin
- Requires camera permission for QR scanning
- Requires NFC permission and hardware for NFC features

## License

This project is created for livestock health management purposes.

