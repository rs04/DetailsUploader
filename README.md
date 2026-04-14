# Contacts Uploader — Android App

A native Android app that reads all contacts from the phone and uploads them to Google Sheets in one tap.

---

## How to Build the APK (Free, No Mac Needed)

### Option A — Build on your PC using Android Studio (Recommended)

1. **Download Android Studio** (free)
   - Go to https://developer.android.com/studio
   - Install it on your Windows/Mac/Linux PC

2. **Open the project**
   - Open Android Studio
   - Click "Open" and select the `ContactsUploader` folder

3. **Build the APK**
   - Wait for Gradle sync to finish (1-2 min first time)
   - Go to **Build → Build Bundle(s) / APK(s) → Build APK(s)**
   - Click "locate" when done — the APK is in `app/build/outputs/apk/debug/`

4. **Share via WhatsApp**
   - Send the APK file directly on WhatsApp to your partners
   - They tap to install (they may need to enable "Install from unknown sources" in Settings)

---

### Option B — Build online using GitHub Actions (No Android Studio needed)

1. Upload this entire `ContactsUploader` folder to a GitHub repository
2. Create `.github/workflows/build.yml` with this content:

```yaml
name: Build APK
on: [push]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-java@v3
        with:
          java-version: '17'
          distribution: 'temurin'
      - name: Build APK
        run: |
          cd ContactsUploader
          chmod +x gradlew
          ./gradlew assembleDebug
      - uses: actions/upload-artifact@v3
        with:
          name: ContactsUploader.apk
          path: ContactsUploader/app/build/outputs/apk/debug/app-debug.apk
```

3. Push to GitHub — it builds automatically
4. Go to **Actions tab → your workflow run → Artifacts** to download the APK

---

## What the App Does

1. Partner opens the app
2. Enters their **name** and **mobile number**
3. Taps **Submit**
4. App requests contacts permission (one-time popup — just tap Allow)
5. All contacts are read silently and uploaded to your Google Sheet instantly
6. No picker, no "select all" — fully automatic after the permission grant

---

## Sharing the APK

- Send via **WhatsApp** directly
- Upload to **Google Drive** and share the link
- Partners need to enable **"Install unknown apps"** from Chrome/WhatsApp in their Android settings

