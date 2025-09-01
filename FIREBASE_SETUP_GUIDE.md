# Firebase Setup Guide for Trimfy Landing Page

## 🚀 Quick Setup Steps

### 1. Create Firebase Project
1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click "Create a project" or "Add project"
3. Enter project name: `trimfy-landing` (or your preferred name)
4. Enable Google Analytics (optional but recommended)
5. Click "Create project"

### 2. Enable Firestore Database
1. In your Firebase project, click "Firestore Database" in the left sidebar
2. Click "Create database"
3. Choose "Start in test mode" (for now - you can secure it later)
4. Select a location close to your users (e.g., `europe-west3` for Spain)
5. Click "Done"

### 3. Get Your Firebase Config
1. Click the gear icon ⚙️ next to "Project Overview"
2. Select "Project settings"
3. Scroll down to "Your apps" section
4. Click the web icon `</>` to add a web app
5. Enter app nickname: `trimfy-web`
6. Click "Register app"
7. Copy the `firebaseConfig` object

### 4. Update Your HTML File
Replace the placeholder config in your HTML with your actual Firebase config:

```javascript
const firebaseConfig = {
  apiKey: "your-actual-api-key",
  authDomain: "your-project-id.firebaseapp.com",
  projectId: "your-project-id",
  storageBucket: "your-project-id.appspot.com",
  messagingSenderId: "your-sender-id",
  appId: "your-app-id"
};
```

### 5. Test the Integration
1. Open your HTML file in a browser
2. Try submitting an email through either form
3. Check the Firebase Console → Firestore Database to see if emails are being collected

## 🔒 Security Rules (Optional but Recommended)

Once you're ready to secure your database, update the Firestore rules:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /emails/{document} {
      allow write: if true;  // Anyone can write emails
      allow read: if false;  // Only you can read (from Firebase Console)
    }
  }
}
```

## 📊 Viewing Collected Emails

1. Go to Firebase Console → Firestore Database
2. You'll see a collection called `emails`
3. Each email submission creates a document with:
   - `email`: The submitted email address
   - `source`: Either "hero" or "peluqueros" (which form was used)
   - `timestamp`: When it was submitted
   - `ip`: Client IP address

## 🎯 Features Added

✅ **Firebase Integration**: Emails are stored in Firestore database
✅ **Form Handling**: Both email forms now submit to Firebase
✅ **Loading States**: Buttons show "Enviando..." while submitting
✅ **Success/Error Notifications**: Beautiful toast notifications
✅ **Source Tracking**: Know which form the email came from
✅ **Timestamp & IP**: Additional metadata for each submission

## 🚨 Important Notes

- **API Keys are Public**: Firebase web API keys are safe to expose in client-side code
- **Test Mode**: Your database starts in test mode (anyone can write)
- **Costs**: Firestore has a generous free tier (50,000 reads, 20,000 writes per day)
- **Backup**: Consider exporting your email list regularly

## 🆘 Troubleshooting

**Emails not being saved?**
- Check browser console for errors
- Verify Firebase config is correct
- Ensure Firestore Database is created and enabled

**Notifications not showing?**
- Check if JavaScript is enabled
- Look for CSS conflicts in browser dev tools

**Need help?**
- Firebase Documentation: https://firebase.google.com/docs
- Firestore Documentation: https://firebase.google.com/docs/firestore

---

Your landing page is now fully connected to Firebase! 🎉
Emails will be collected and stored securely in your Firestore database.
