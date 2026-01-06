# 📱 Android APK Static Testing Guide

This guide explains how to perform **static analysis of an installed Android application** using **ADB and JADX**, commonly used during **Android Mobile VAPT**.

---

## ⚠️ Disclaimer

This guide is intended strictly for **educational and authorized security testing purposes**.  
Perform these steps **only on applications and devices you own or have explicit permission to test**.

---

## 🧪 Prerequisites

- Android device with **Wireless Debugging enabled**
- ADB installed on host machine
- JADX (GUI or CLI)
- Target application installed on the device

---

## 🔌 Step 1 — Connect Device Using Wireless Debugging

Ensure your Android device is connected to your host machine using **Wireless Debugging** and visible via:

```bash
adb devices
```

---

## 📦 Step 2 — Get APK Path of Installed Application

Open terminal and run:

```bash
adb shell pm path com.packagename
```

You will receive output similar to:

```
package:/data/app/~~xyz/base.apk
```

Copy the **complete APK path**.

---

## ⬇️ Step 3 — Pull APK from Device

Use the copied path to pull the APK to your host machine:

```bash
adb pull /data/app/~~xyz/base.apk
```

The `base.apk` file will be copied to your local system.

---

## 🔍 Step 4 — Analyze APK Using JADX

1. Open **JADX**
2. Load the extracted `base.apk`
3. Navigate to:

```
Resources → AndroidManifest.xml
```

4. Start analyzing:
   - Exported activities, services, receivers
   - Permissions
   - SDK versions
   - Debug flags
   - Deep links

---

## 📂 Step 5 — Analyze App Data Directory

Open ADB shell:

```bash
adb shell
```

Navigate to the app’s data directory:

```bash
cd /data/data/com.packagename
```

Analyze contents such as:
- Databases (`databases/`)
- Shared preferences (`shared_prefs/`)
- Cache files
- Logs
- Configuration files

> ⚠️ Access may require root privileges.

---

## 📜 Step 6 — Fetch Application Logs

To fetch runtime logs related to the application:

```bash
logcat | grep "appname"
```

Use this to identify:
- Sensitive information leakage
- Debug logs
- API keys
- Authentication tokens
- Error messages

---

## 📚 Use Cases

- Android Mobile VAPT
- Static code and configuration analysis
- Sensitive data exposure checks
- Reverse engineering preparation
- Permission and component analysis

---

## 📝 Notes

- This method does **not require the original APK**
- APK paths may differ across Android versions
- Root access improves visibility but is not always mandatory
- Combine static testing with dynamic analysis for better coverage

---

## 📜 License

This guide is intended for **educational and authorized security testing purposes only**.
