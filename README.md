# Mayar Jobs Afghanistan

A mobile-first, trilingual (Dari Afghanistan, Pashto, English) static job-board starter.

## Files
- `index.html`: app layout and modals
- `style.css`: responsive UI
- `app.js`: language switching, search/filter, job details, WhatsApp contact, CV print-to-PDF, local admin draft
- `jobs.json`: published job listings
- `manifest.json`, `icon.svg`: installable web-app metadata/icon

## Publish with GitHub Pages (phone-friendly)
1. Create a public repository named `mayar-jobs-afghanistan`.
2. Upload all files in this folder to the repository root. Keep filenames exactly as shown.
3. Open repository **Settings → Pages**.
4. Under **Build and deployment**, select **Deploy from a branch**.
5. Select branch `main`, folder `/(root)`, then **Save**.
6. Wait for deployment, then open the Pages URL shown in Settings → Pages. Test the URL on your phone.

Do not open `index.html` directly as a local file; the app fetches `jobs.json`, which requires a web server.

## How the admin draft works
This is a static website. Job listings visible to everyone are in `jobs.json`. The in-page admin uses demo PIN `1234` and is **not secure**; it is only a local drafting helper. Changes in it are stored in browser memory and are not sent to GitHub or other visitors.

To publish a job:
1. Open the published site and tap **مدیریت / Admin**.
2. Enter demo PIN `1234`, add or remove jobs, then tap **Export/show jobs JSON**.
3. Download the generated `jobs.json`.
4. In your GitHub repository, open `jobs.json`, tap Edit (pencil), replace the whole content with the exported JSON, then **Commit changes**.
5. Wait for GitHub Pages to redeploy. Check the public site.

If downloads are awkward on your phone, copy the JSON shown in the new tab and paste it into GitHub's `jobs.json` editor. For the first real launch, remove all sample listings and publish only verified jobs. Never publish a fake job or a private person's contact details without permission.

## WhatsApp numbers
Use digits only with country code, no plus sign, spaces, or dashes. Example format for Afghanistan: `937XXXXXXXX`. Verify the number belongs to the employer before publishing.

## CV builder
The CV builder opens a print window. Select **Save as PDF** in the browser print dialog if available. If pop-ups are blocked, allow pop-ups for the site.

## Important limitations
- GitHub Pages hosts static files; it does not provide user accounts, private admin access, a database, or secure form submissions.
- The demo PIN is visible in `app.js`. Anyone can inspect client-side code. Do not use it to protect confidential administration.
- No online payments or paid-job claims are built in.
- This is a website/PWA, not an APK yet.

## Turning it into an Android APK
The simplest route is to first publish and test the website. For an APK, create a separate Android wrapper project using Android Studio/Gradle with a WebView pointing to the published HTTPS GitHub Pages URL, then build the debug APK using GitHub Actions. This requires Android project files (`settings.gradle`, root `build.gradle`, `app/build.gradle`, Android manifest, and Java/Kotlin Activity); those are not the same as the static website files in this ZIP. A safer production option is to package a PWA with a Trusted Web Activity, which requires an Android build setup and domain verification. Do not paste the website files into a random APK builder and expect it to work automatically.

## Suggested next version
For secure remote admin publishing, connect a backend/database such as Supabase or Firebase and implement proper authentication and validation. Review its free-tier limits before use.

## Included Android wrapper project
The `android-wrapper/` folder contains a minimal WebView Android project and a GitHub Actions workflow.

1. First publish the website and note the exact Pages URL.
2. In `android-wrapper/app/src/main/java/af/mayar/jobs/MainActivity.java`, replace `https://YOUR-GITHUB-USERNAME.github.io/mayar-jobs-afghanistan/` with your real URL.
3. In the same file, replace `YOUR-GITHUB-USERNAME.github.io` in the host check with your actual GitHub Pages host, for example `myaccount.github.io`.
4. Upload the `android-wrapper/` folder into the same repository, keeping its folders intact.
5. Open GitHub → Actions → **Build Mayar Jobs APK** → **Run workflow**.
6. When the workflow completes, open its run page, scroll to Artifacts, and download `mayar-jobs-debug-apk`. Extract the ZIP to get `app-debug.apk`.
7. This is a debug APK for testing. A public production release should be signed securely before distribution.

If Gradle/Android SDK errors appear, open the failed Actions run and read the first red error. GitHub Actions builds can take several minutes.
