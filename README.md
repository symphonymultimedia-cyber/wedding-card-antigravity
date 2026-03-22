# Wedding Invitation Flutter Web App

## Requirements
- [Flutter SDK](https://docs.flutter.dev/get-started/install) installed.
- [Firebase CLI](https://firebase.google.com/docs/cli) installed (`npm install -g firebase-tools`).

## Setup Instructions

1. **Install Dependencies**
   Open your terminal in this directory and run:
   ```bash
   flutter pub get
   ```

2. **Configure Firebase**
   You need to link this app to your Firebase project. Ensure you are logged into Firebase CLI:
   ```bash
   firebase login
   dart pub global activate flutterfire_cli
   flutterfire configure --project=YOUR_FIREBASE_PROJECT_ID
   ```
   *This will automatically update the `lib/firebase_options.dart` file with your real keys.*

3. **Enable Firebase Services**
   In your Firebase Console, make sure you enable:
   - **Authentication**: Enable Email/Password sign-in (create your admin user here).
   - **Firestore Database**: Create a database and set up security rules (allow read for everyone, write only if authenticated).

   Example Firestore Rules:
   ```text
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       // Allow anyone to read live updates
       match /live_updates/{document=**} {
         allow read: if true;
         // Only authenticated admin can write
         allow write: if request.auth != null;
       }
     }
   }
   ```

4. **Run the App locally**
   ```bash
   flutter run -d chrome
   ```

5. **Deploy to Firebase Hosting**
   ```bash
   flutter build web
   firebase init hosting
   firebase deploy --only hosting
   ```

## Assets Note
The photos and videos in the code are currently placeholders using Unsplash and Flutter docs respectively, as direct Drive extraction for media elements requires API keys or direct download links. 
To use your specific Google Drive assets:
- For Images: Get direct download URLs for your pre-wedding photos or upload them to Firebase Storage, then replace the URLs in `lib/pages/home_page.dart`.
- For Videos: Replace the URLs in the `_buildVideoSection` in `home_page.dart` with direct MP4 links (or upload the parent videos to Firebase Storage).
