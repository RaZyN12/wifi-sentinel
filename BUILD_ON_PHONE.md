# Build the APK using only your Android phone

This project includes a GitHub Actions cloud-build workflow. You do not need a PC, but you do need a GitHub account and a browser on your phone.

1. Sign in to GitHub in your phone browser.
2. Create a new repository named `wifi-sentinel`. Keep it private if you prefer.
3. Upload the contents of this ZIP to the repository (upload the files and folders inside `WIFI_SENTINEL`, not the outer folder).
4. Open the repository's **Actions** tab.
5. Select **Build WIFI SENTINEL APK** and tap **Run workflow**. If the workflow already ran after upload, open the latest run instead.
6. Wait for the workflow to finish. Open the completed run and find **Artifacts** near the bottom.
7. Download `WIFI-SENTINEL-debug-apk`, extract it on your phone, then tap `app-debug.apk` to install.
8. If Android blocks installation, allow your browser or file manager to install unknown apps for this one installation.

The workflow builds a debug APK and runs JVM unit tests. A successful cloud build does not guarantee every Wi-Fi scan feature works on every custom ROM. Test on your own S10+.

If uploading folders through GitHub mobile is difficult, use GitHub's browser desktop-site option. Do not publish signing keys, passwords, or personal network data in the repository.
