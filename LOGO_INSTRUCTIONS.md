# How to Add Your Custom Logo Image

## Where to Save Your Logo Image

1. **Create/Open the drawable folder:**
   ```
   app/src/main/res/drawable/
   ```

2. **Save your logo image file:**
   - Name it: `app_logo.png` (or `app_logo.jpg`)
   - Recommended size: 512x512 pixels or larger
   - Format: PNG (with transparency) or JPG

3. **After saving the image**, update the LoginScreen code:

## Update Code

After saving `app_logo.png` in `app/src/main/res/drawable/`, update `LoginScreen.kt`:

**Find this line (around line 82-87):**
```kotlin
androidx.compose.foundation.Image(
    painter = painterResource(id = R.drawable.ic_launcher_foreground),
    contentDescription = "VetNxt Logo",
    modifier = Modifier.size(100.dp),
    contentScale = ContentScale.Fit
)
```

**Change it to:**
```kotlin
androidx.compose.foundation.Image(
    painter = painterResource(id = R.drawable.app_logo),
    contentDescription = "VetNxt Logo",
    modifier = Modifier.size(100.dp),
    contentScale = ContentScale.Fit
)
```

## Quick Steps:
1. Copy your logo image file
2. Navigate to: `app/src/main/res/drawable/`
3. Paste the file and name it: `app_logo.png`
4. Update the code reference from `R.drawable.ic_launcher_foreground` to `R.drawable.app_logo`
5. Sync Gradle and rebuild

## Alternative: Using Vector Drawable
If you have an SVG logo, you can convert it to Android Vector Drawable format and save it as `app_logo.xml` in the same `drawable` folder.

