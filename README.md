# DrawingJoy — Private Drawing App for Android

A simple, private, offline whiteboard-style drawing app. No login, no accounts,
no ads, no tracking. Open → Draw → Save → Record → Share.

## What's inside

- A full Android Studio project (Kotlin), source in `app/src/main/java/com/mom/privatedrawing/`
- On first launch, a quick "Phone or Tablet?" picker that sizes the side panel
  and toolbar appropriately (changeable later by clearing app data)
- A left-side color palette with a custom color wheel picker and a saved
  "My Colors" section (stored locally on the device)
- Pen, Pencil, Marker, Highlighter, Brush (soft/textured), Eraser, Fill, Text,
  Line, Rectangle, Circle, Triangle, Star, and Image import tools
- A dedicated Text mode: selecting Text swaps the side panel to font, size,
  and color controls, then a tap on the canvas prompts for the words
- Undo / Redo / Clear (with confirmation)
- Save as PNG (canvas only, no toolbar) to the gallery. Saving prompts you to
  name the drawing, shows a "Drawing saved" confirmation, and adds it to
  "My Drawings"
- "My Drawings": search saved drawings by name, then tap one to View (full-size
  preview), Edit (reopen it on the canvas and keep drawing), Share, or Delete it
- Share via any installed app
- Recording to MP4 with a record → pause/resume → stop (heptagon button)
  flow, a visible recording indicator and timer, and a Save/Share/Delete
  prompt once you stop. Recording captures only the drawing canvas itself
  (directly, via the device's video encoder) — there is no "cast your whole
  screen" system permission dialog, and nothing outside the canvas is ever
  captured
- A Full-Screen mode that hides the side panel and toolbar
- `.github/workflows/build-apk.yml` — builds a debug APK automatically in
  GitHub's free cloud runners, no paid service, nothing published to the Play
  Store

**Honesty notes on a few things that have real technical limits:**
- Pause and resume on a recording are handled entirely by the app itself
  (not the phone's video encoder), so they work the same reliable way on
  every device.
- "My Drawings" saves a flattened image of the canvas, not the individual
  strokes — so reopening a drawing lets you keep drawing on top of it, but
  undo/redo after reopening only affects what you add from that point
  forward, not the original strokes.

---

## Step 1 — Put the project on GitHub

1. Go to https://github.com and log in (create a free account if you don't
   have one).
2. Click the **+** in the top-right corner → **New repository**.
3. Name it something like `my-drawing-board`, keep it **Private** (recommended,
   since this is for personal/family use), and click **Create repository**.
4. On the new repo's page, click **uploading an existing file** (or, if you're
   comfortable with git on your computer, use the command line instead — see
   the box below).
5. Drag the **entire contents** of this project folder in (keep the folder
   structure — `app/`, `.github/`, `build.gradle`, etc.) and commit.

**Command-line alternative**, run from inside this project folder:
```bash
git init
git add .
git commit -m "Initial commit: private drawing app"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/my-drawing-board.git
git push -u origin main
```

## Step 2 — Run the GitHub Actions build

The workflow is already set to run automatically as soon as you push to the
`main` branch, so simply completing Step 1 will kick it off. To trigger it
manually instead (or run it again):

1. In your repository on GitHub, click the **Actions** tab.
2. Click **Build APK** in the left sidebar.
3. Click **Run workflow** → **Run workflow**.
4. Wait a few minutes — you'll see a spinning yellow icon that turns into a
   green check mark when the build succeeds.

## Step 3 — Download the APK

1. In the **Actions** tab, click on the finished workflow run (the one with
   the green check mark).
2. Scroll down to the **Artifacts** section at the bottom of that page.
3. Click **private-drawing-app-debug-apk** to download it as a `.zip` file.
4. Unzip it — inside you'll find `app-debug.apk`.

## Step 4 — Install it on your mother's Android phone

1. Get `app-debug.apk` onto her phone (email it to yourself and open the
   attachment on her phone, use a USB cable, share it via a messaging app, or
   upload it to Google Drive and download it on the phone — any method
   works).
2. On her phone, tap the APK file to install it.
3. Android will likely show a warning like "install blocked" or "unknown
   source" the first time — this is normal for any app installed outside the
   Play Store. Tap **Settings** in that prompt, allow installs from that
   source (e.g. Files, Chrome, or Gmail — whichever app you used), then go
   back and tap install again.
4. Once installed, open **DrawingJoy** from the home screen. No sign-up,
   no setup — it goes straight to the drawing screen.

That's it: Open → Draw → Save → Record → Download → Share.

---

## Notes for future changes

- The app is unsigned (uses the standard Android debug key), which is normal
  and fine for private, non-Play-Store installs — it just means each fresh
  install replaces the last one cleanly.
- All custom colors are stored in `SharedPreferences` on-device only.
- All drawings save to `Pictures/DrawingJoy` in the phone's normal gallery.
- All recordings save to the app's private storage and are only accessible
  through the app's own Share/Delete options, or via a file manager.
- Nothing in this app calls the internet, and no analytics or ad SDKs are
  included anywhere in the project.
