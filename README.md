# Public Message Board

A responsive, real-time public message board. Visitors can publish multiple messages; all visitors see the same live list. Anyone can delete any message.

## Before you begin

You need a Google account and a computer with Node.js installed. The Firebase setup is free to start, but Google may require a billing account for some services or usage levels. Keep an eye on Firebase usage and quotas.

## 1. Create a Firebase project

1. Open https://console.firebase.google.com/ and choose **Add project**.
2. Give it a project name, then complete the setup.
3. In the project overview, click the Web icon (`</>`) to register a web app.
4. Give the app a nickname and register it. Firebase displays a `firebaseConfig` object.
5. Copy the values into the `firebaseConfig` object near the bottom of `index.html`, replacing all `PASTE_...` values.

The web config is intended to be included in a website. It is not a server password. The Firestore security rules are what define access.

## 2. Create the database

1. In Firebase Console, open **Build → Firestore Database**.
2. Click **Create database**.
3. Choose production mode and select a database location near your audience.
4. After it is created, open the **Rules** tab.
5. Replace the rules with the full contents of this project's `firestore.rules` file and click **Publish**.

Important: these rules intentionally allow anyone on the internet to read all messages, publish messages, and delete any message. Do not use this setup for private, sensitive, or confidential information. Anyone can also delete every post. There is no undo or admin-only recovery in this version.

## 3. Test locally (optional)

You can deploy directly after configuration. To test locally, install the Firebase CLI:

```bash
npm install -g firebase-tools
firebase login
```

From this project folder, run:

```bash
firebase use --add
```

Choose the Firebase project you created. Then:

```bash
firebase emulators:start --only hosting
```

Open the local URL shown in the terminal. (For a full local Firestore test, configure and start the Firestore emulator too.)

## 4. Deploy the website

In a terminal, change into this project folder and run:

```bash
npm install -g firebase-tools
firebase login
firebase use --add
firebase deploy
```

When `firebase use --add` asks for a project, select the same project used for your web app. If you already selected it once, you do not need to repeat that command.

Firebase prints a Hosting URL, usually:

`https://YOUR_PROJECT_ID.web.app`

Share that URL with anyone. They can open the same board from their phone or computer.

## 5. Updating the site

Edit `index.html`, then run:

```bash
firebase deploy --only hosting
```

If you change `firestore.rules`, publish them in Firebase Console or run:

```bash
firebase deploy --only firestore:rules
```

## Notes and limitations

- Messages are stored in Cloud Firestore, not in a visitor's browser.
- New posts and deletions appear live for everyone with the page open.
- The board sorts newest first.
- A message can contain up to 5,000 characters.
- Anyone can delete any message, as requested. A malicious visitor could erase the board.
- This starter version has no sign-in, moderation, spam protection, or message-editing feature. For a public site, consider adding CAPTCHA/app check, rate limits, moderation, and an admin recovery process before sharing widely.
