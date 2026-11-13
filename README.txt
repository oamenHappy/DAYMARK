DAYMARK v2 — GOOGLE DRIVE BACKUP

Files: index.html, manifest.json, sw.js.

IMPORTANT: This version preserves the existing IndexedDB database name and object store. Deploy it over the existing site using the same origin (same protocol + hostname + port) and do NOT clear browser/site data. Existing local activities should remain available.

SET UP GOOGLE DRIVE
1. Open https://console.cloud.google.com/ and create/select a Google Cloud project.
2. Enable Google Drive API for the project.
3. Configure Google Auth Platform / OAuth consent screen with app name Daymark and your email.
4. Create OAuth client credentials: Create client > Web application.
5. Add your exact website origin under Authorized JavaScript origins (example: https://YOURNAME.github.io). Do not add a path.
6. Copy the OAuth Client ID (ends in .apps.googleusercontent.com).
7. Open Daymark on its HTTPS website, paste the Client ID into the Google Drive backup section, and tap Connect Google Drive.
8. Approve access. Daymark creates/updates daymark-backup.json in your Drive.

SECURITY AND LIMITATIONS
- The app requests the narrow drive.file scope, which allows it to create/manage files it creates or opens, not read your whole Drive.
- No Google password or client secret is stored in the website. OAuth access tokens stay in memory only.
- Local changes are automatically uploaded while the Google access token remains valid. Google browser access tokens expire; after reloading Daymark or when access expires, tap Connect Google Drive again. A static GitHub Pages site cannot safely hold a long-lived refresh token or perform unattended background uploads. For fully unattended sync across sessions, add a trusted backend using Google's authorization-code flow and securely store refresh tokens server-side.
- First connection: if Drive has a backup and this browser has no activities, Daymark restores it. If both have activities, it merges by date + category + title and keeps completed status if either copy is completed, then uploads the merged backup.
- This is a simple single-file backup/sync design, not a conflict-free multi-user database. Concurrent edits/deletions across multiple devices may need a more advanced sync backend. Keep periodic Export backup copies too.
- Google OAuth may show an unverified-app warning while the project is in testing. Add your Google account as a test user in the OAuth audience settings.
