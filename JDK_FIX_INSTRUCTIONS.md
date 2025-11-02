# JDK Compatibility Fix Instructions

## Problem
The build is failing with a `jlink.exe` error, which is a known issue with JDK 21 and Android Gradle Plugin 8.1.0.

## Solution: Use JDK 17 for Gradle

### Method 1: Configure in Android Studio (Easiest)

1. Open Android Studio
2. Go to **File → Settings** (Windows/Linux) or **Android Studio → Preferences** (macOS)
3. Navigate to: **Build, Execution, Deployment → Build Tools → Gradle**
4. Under **Gradle JDK**, select:
   - `jbr-17` (JetBrains Runtime 17) - if available
   - Or `17` - if you have JDK 17 installed
   - Or `Embedded JDK` (try this if others don't work)
5. Click **Apply** and **OK**
6. Click **Sync Project with Gradle Files** (or File → Sync)

### Method 2: Clean and Rebuild

After changing the JDK:

1. **File → Invalidate Caches / Restart**
   - Select "Invalidate and Restart"
   
2. Or manually clean:
   - **Build → Clean Project**
   - **Build → Rebuild Project**

### Method 3: If JDK 17 is Not Available

If Android Studio doesn't have JDK 17:

1. Download JDK 17 from:
   - [Oracle JDK 17](https://www.oracle.com/java/technologies/javase/jdk17-archive-downloads.html)
   - Or [OpenJDK 17](https://adoptium.net/temurin/releases/?version=17)

2. Install it

3. In Android Studio:
   - **File → Settings → Build, Execution, Deployment → Build Tools → Gradle**
   - Click the **...** button next to Gradle JDK
   - Select **Download JDK** or **Add JDK**
   - Choose JDK 17

### Alternative: Downgrade Android Gradle Plugin (Not Recommended)

If the above doesn't work, you could try updating to a newer Android Gradle Plugin version that better supports JDK 21, but using JDK 17 is the recommended solution.

## Verification

After applying the fix, try building again. The error should be resolved.

If you still see errors, share the new error message.

