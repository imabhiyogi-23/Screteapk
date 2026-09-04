# Rahasya Vault — Android App

This is the real, installable Android version of Rahasya Vault, built with Capacitor.
Unlike the website version, this one can actually ask Android to delete the original
photo/video from your phone's gallery after it's safely encrypted into the vault —
because it's a real app with real storage permissions, not a page in a browser.

## How deletion actually works

After a photo or video is imported and encrypted, the app asks Android's system
delete confirmation dialog to remove the original. **You still tap "Allow" or "Delete"
on a real Android system popup** — no app, including this one, is allowed to silently
delete your files. That confirmation step is an Android privacy protection, not a
limitation of this app.

## Get the APK without installing Android Studio

This repo includes a GitHub Actions workflow that builds the app on GitHub's own
servers every time you push.

1. Push this whole folder to a new GitHub repository.
2. Go to the repo's **Actions** tab. A workflow called "Build Android APK" should
   run automatically (or click **Run workflow** to trigger it manually).
3. Wait for it to finish (a few minutes).
4. Open the finished run, scroll to **Artifacts**, and download
   `rahasya-vault-debug-apk`. Unzip it — inside is `app-debug.apk`.
5. Copy `app-debug.apk` to your phone (via USB, Google Drive, WhatsApp to yourself,
   etc.) and tap it to install. Android will warn about "installing from unknown
   sources" the first time — that's expected for an app not from the Play Store;
   allow it for this one file.

## Building it yourself instead (optional)

If you'd rather build locally with Android Studio:

```bash
npm install
npx cap sync android
npx cap open android
```

Then use Android Studio's **Build → Build Bundle(s)/APK(s) → Build APK(s)**.

## Project layout

- `www/` — the vault web app itself (same app as the website version)
- `android/` — the native Android project (Gradle, manifest, the custom plugin)
- `android/app/src/main/java/studio/swalavya/rahasya/GalleryCleanupPlugin.java` —
  the native plugin that opens the system picker and requests deletion of originals
- `.github/workflows/build-apk.yml` — builds the APK automatically on GitHub

## Notes

- This produces a **debug** build, which is fine for installing on your own phone.
  A Play Store release would need a signed release build — a separate step if you
  ever want to publish it there.
- The app icon currently uses Capacitor's default placeholder. Swap the images in
  `android/app/src/main/res/mipmap-*/` with your own if you want custom branding.
