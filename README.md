# TaskPole — Official Releases

**This is the official home of the TaskPole Android app, published by NERD LLC —
the same people who run [taskpole.com](https://taskpole.com).**

Every file released here is built from our private source repository, signed
with our release key, and published with a SHA-256 checksum so you can prove,
yourself, that the file you downloaded is the file we built. Nothing else is
uploaded to this repository.

## Download

### → [taskpole.com/download/android](https://taskpole.com/download/android)

That link always resolves to the newest release below. It is the only download
link we publish.

**If you were given a TaskPole APK from anywhere else — a file-sharing site, a
third-party "APK mirror", a chat message, an email attachment — do not install
it.** We cannot vouch for it, and a modified build signed with someone else's
key can do anything it likes with your account. Use the link above, or the
Releases page on this repository. Nothing else is us.

## "Android says this file may be harmful" — what's going on

You will see a warning the first time you install this. That is expected, and it
is not a statement about our app.

TaskPole is distributed **directly**, not through the Google Play Store, so
Android asks you to confirm that you trust the source. The prompt says something
like *"For your security, your phone is not allowed to install unknown apps from
this source"*, and you allow it once for the browser you downloaded with. Google
Play Protect may also scan the file and note that it was not installed from
Play.

Both are the operating system doing its job on a file it has not seen before.
Neither means anything was detected. If you would rather not take our word for
it, verify the file yourself — that is what the next section is for, and it is
better evidence than any reassurance we could write.

## Verify what you downloaded

Two independent checks. The first proves the bytes were not altered; the second
proves **we** are the ones who signed them.

### 1. The checksum

Every release has a `taskpole.apk.sha256` file attached beside the APK, and the
same hash is printed in the release notes.

```bash
shasum -a 256 taskpole.apk        # macOS / Linux
certutil -hashfile taskpole.apk SHA256   # Windows
```

The value must match the release exactly. If it does not, delete the file and
download it again from the link above.

### 2. The signature

The checksum proves the file is intact. The signature proves it is *ours*. Every
TaskPole release — past, present and future — is signed with this certificate:

```
SHA-256  AA:A9:4B:ED:37:D1:C1:E0:A3:08:24:C5:25:40:E2:6A:14:FD:46:0C:4D:CB:76:E7:94:27:DF:89:A2:BC:BC:EC
```

Check it with the Android SDK's `apksigner`:

```bash
apksigner verify --print-certs taskpole.apk
```

This fingerprint does not change between versions. **A TaskPole APK that shows a
different fingerprint was not built by us** — no matter where you got it or what
the file is called. Android enforces the same rule: a build signed with a
different key cannot install over one signed with ours.

You can also confirm the fingerprint independently, from our website rather than
from this page: <https://taskpole.com/.well-known/assetlinks.json>

## What the app can access

TaskPole requests five Android permissions, and you can confirm this list
against any release with `aapt dump permissions taskpole.apk`:

| Permission | Why |
|---|---|
| `INTERNET` | talk to taskpole.com — the app is an interface to your account |
| `POST_NOTIFICATIONS` | show your task reminders |
| `VIBRATE` | let a reminder buzz |
| `WAKE_LOCK` | deliver a reminder scheduled while the phone is idle |
| `RECEIVE_BOOT_COMPLETED` | restore your scheduled reminders after a restart |

Four of the five exist solely to deliver reminders. **The app does not request
location, contacts, camera, microphone, photos, files, SMS, or call history**,
and cannot access them.

Your data lives in your TaskPole account, governed by the
[Privacy Policy](https://taskpole.com/privacy) and
[Terms of Use](https://taskpole.com/terms). The app is a client for that
account — deleting it removes nothing from your account, and you can delete the
account itself from within the app.

## Requirements

| | |
|---|---|
| Android | 6.0 (Marshmallow, API 23) or newer |
| Package | `com.taskpole.app` |
| Size | roughly 4.5 MB |
| Account | a free TaskPole account — [sign up](https://taskpole.com/register) |

## Updates

**There is no automatic update.** Because this app is installed directly rather
than through Play, your phone will not offer you new versions. To update, come
back to [taskpole.com/download/android](https://taskpole.com/download/android)
and install the newer file over the top.

Updating in place keeps everything — you are not signed out and nothing local is
lost — because the new build is signed with the same key as the one you already
have. You never need to uninstall first, and you should be suspicious of any
"TaskPole update" that tells you to.

## About this repository

It holds **releases only**: the signed APK and its checksum, one tag per
version. There is no source code here — TaskPole's source is private — and no
issue tracker.

- **Support, questions, bug reports:** <support@taskpole.com>
- **Security or anything that looks like an impersonation of this app:** email
  <support@taskpole.com> and say so in the subject line. If you have found an
  APK claiming to be TaskPole with a different signing fingerprint, we want to
  know about it.

---

© NERD LLC · [taskpole.com](https://taskpole.com)
