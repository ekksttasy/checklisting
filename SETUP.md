# Checklisting — one-time setup

We're using Firebase (Google's app backend service) because it gives you
real email/password accounts and a live database without you having to
run or self-host a server. This is a one-time, ~10 minute setup.

## 1. Create a Firebase project
1. Go to https://console.firebase.google.com and sign in with any Google account (a fresh one for the business is fine).
2. Click **Add project**, name it something like `rundown-app`, and finish the wizard (Google Analytics is optional — you can skip it).

## 2. Turn on Email/Password sign-in
1. In the left sidebar: **Build → Authentication → Get started**.
2. Under **Sign-in method**, click **Email/Password**, enable it, click **Save**.

## 3. Create the database
1. Left sidebar: **Build → Firestore Database → Create database**.
2. Choose **Start in production mode**, pick a region close to your business, click **Enable**.
3. Once created, go to the **Rules** tab and replace the contents with what's in `firestore.rules` (added in Phase 2, once groups/checklists exist). For now the default production rules are fine — Phase 1 doesn't write shared data yet.

## 4. Get your config and paste it in
1. Left sidebar gear icon → **Project settings**.
2. Under "Your apps," click the **</>** (web) icon to register a web app. Name it anything, skip hosting for now.
3. Firebase shows you a `firebaseConfig` object. Copy it.
4. Open `index.html`, find `FIREBASE_CONFIG` near the bottom, and paste your values in place of the placeholders.

## 5. Try it
Open `index.html` by double-clicking it (or drag it into a browser tab). You should see the Rundown login screen with no warning banner. Create an account — you'll land on the app shell.

## 6. When you're ready to give users a link
A file on your computer only works for you. To get a real link users & group leaders can open on their phones:
- Firebase Hosting (free). In a terminal: `npm install -g firebase-tools`, then `firebase login`, `firebase init hosting` (point it at the folder with `index.html`), then `firebase deploy`. You'll get a `https://your-project.web.app` link.
- Any other static host works too (Netlify, Vercel, S3).
- Once it's on a real link, users open it in Safari/Chrome on their phone and can **Add to Home Screen** — it behaves like an installed app, no App Store needed.

## About "sending an invite"
Firebase's free client-side tools can't have a group leader create a
password for someone else remotely.Instead: a leader creates a group and gets a
short join code; they text/tell it to new group members along with the app
link; group members create their own account and enter the code to join.
