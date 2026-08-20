---
manufacturer:
    - ulefone

---

## Auto-Start and Background Usage

Look in your system Settings for **Manage Apps Automatically** or **App Launch** in Battery (or Battery Manager) and disable restrictions on the apps you depend on daily.

Inside this menu, you will see a master toggle at the top that says **Manage all automatically**. Turn that master toggle OFF.
Once turned off, a list of your individual apps will appear. Find your app, tap it, and ensure it is set to Manage Manually. Make sure **Auto-launch**, **Secondary launch** (apps launching other apps), and **Run in background** are all explicitly turned ON.

## Adjust Battery Permissions for Specific Apps

If you have an app that you want to always run in the background:

Go to Settings → Apps → [App Name] → Battery. Set it to Unrestricted (or "Unlimited") to prevent the operating system from putting it to sleep.


## DuraSpeed (App Killer)

DuraSpeed is a built-in MediaTek software layer meant to boost the foreground app by starving background processes. 

The  custom interface relies heavily on the DuraSpeed system app to throttle background processes, which frequently delays messaging app notifications.
Turn it off: Go to Settings → DuraSpeed and toggle it off completely. This solution, however, seems to be only temporary and changes on its own by the phone.

**Advanced workaround:** If the feature aggressively overrides your app settings, you can remove it using the Canta app and Shizuku via an ADB connection (see below)


## Another Killer

A known quirk is that DuraSpeed and a hidden process called Screen Off Killer (com.pri.screenoff.killer) will often silently turn themselves back on or reset your "Unrestricted" apps to "Optimized".
To permanently kill the killers without needing to root your device, you can use an ADB (Android Debug Bridge) environment on your phone using Shizuku and an open-source uninstaller called Canta.

### Step 1: Set Up Shizuku (On-Device ADB)

1. Download **Shizuku** from the Google Play Store.
2. Go to Settings → About Phone and tap Build Number 7 times until it says "You are now a developer."
3. Go back to main settings, enter System → Developer Options, and enable USB Debugging and Wireless Debugging.
4. Open Shizuku, tap Pairing, go to Wireless Debugging settings, tap *Pair device with pairing code, and enter that code into the Shizuku notification.
5. Tap Start in the main Shizuku app.

### Step 2: Use Canta to Freeze the Aggressive Daemons

1. Download and install Canta (available on F-Droid or GitHub).
2. Open Canta and grant it permission to hook into Shizuku.
3. Tap the three-dot menu in Canta and ensure Only System or system packages are visible.
4. Search for the following two packages:
    * **DuraSpeed** (com.mediatek.duraspeed or similar variant)
    * **Screen Off Killer** (com.pri.screenoff.killer)
5. Select them and tap the Trash Can icon to uninstall/disable them for the current user.

⚠️ Note: Because Canta uninstalls these via the --user 0 ADB command, it is  safe. The apps are removed from your active profile so they can't run, but they won't brick your phone, and a factory reset will bring them back if you ever need them.
