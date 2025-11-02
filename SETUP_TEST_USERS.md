# Setting Up Test Users

To test the app, you'll need to create user accounts in the database. Here are two ways to do this:

## Option 1: Add Users Programmatically (Recommended for Testing)

Add this code to `MainActivity.onCreate()` temporarily to create test users:

```kotlin
// Add this to onCreate() after initializing repository
lifecycleScope.launch {
    // Create test villager
    repository.insertUser(
        User(
            loginId = "villager1",
            password = "pass123",
            role = "villager",
            name = "Raju Kumar",
            phone = "9876543210",
            village = "Wardha"
        )
    )
    
    // Create test doctor
    repository.insertUser(
        User(
            loginId = "doctor1",
            password = "pass123",
            role = "doctor",
            name = "Dr. Sharma",
            phone = "9876543211"
        )
    )
}
```

Remove this code after first run to avoid duplicates.

## Option 2: Create Users via Database Inspector

1. Run the app in debug mode
2. Go to **View → Tool Windows → App Inspection → Database Inspector**
3. Navigate to `livhealth-db` → `users` table
4. Click **+** to add a new row
5. Fill in the fields:
   - `loginId`: unique identifier (e.g., "villager1")
   - `password`: plain text password (e.g., "pass123")
   - `role`: either "villager" or "doctor"
   - `name`: user's name
   - `phone`: optional phone number
   - `village`: optional village name

## Test Credentials

### Villager Account
- **Login ID**: `villager1`
- **Password**: `pass123`
- **Role**: Villager

### Doctor Account
- **Login ID**: `doctor1`
- **Password**: `pass123`
- **Role**: Doctor

## Testing Workflow

1. **Login** as a villager and add animals
2. **Logout** and **login** as a doctor
3. **Scan QR** code from an animal to inspect it
4. **Fill inspection form** and submit
5. **View inspected animals** list

## Notes

- Passwords are stored in plain text for simplicity (implement encryption for production)
- QR codes should contain the Animal ID for scanning to work
- NFC tags should contain Animal ID in NDEF text format

