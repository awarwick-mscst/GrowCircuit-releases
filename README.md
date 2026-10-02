# 🌱 GrowCircuit

**A grow journal and grow room monitor for Windows that keeps everything on
your own computer.**

GrowCircuit keeps the record of every grow: when it started, when it flipped
to flower, when it came down, and everything in between, from each watering
and feed to the temperature and humidity off your gauge, training, problems
and photos. A cheap thermometer and hygrometer is all the hardware it needs.
Add GrowCircuit sensors and it logs the room for you around the clock.

It is free, with no account, no subscription and no cloud.

**[⬇ Download the latest version](https://github.com/awarwick-mscst/GrowCircuit-releases/releases/latest)**

This repository holds the installers and release notes only.

---

## What it does

- **A journal for every grow.** Tap what you did (watered, fed, trained,
  defoliated, transplanted, spotted a problem), add the water's amount, pH
  and PPM, a reading, a note and a photo, and it all lands in one timeline,
  grouped by week of veg or flower.
- **A daily check-in** on the home screen: when you last watered, logged a
  reading and took a photo, and what is worth doing today.
- **Many grows at once**, in rooms of their own. Each grow has a veg start,
  a flower start and a harvest date, and the phase and day count follow:
  set the date and "day 39 of flower" is worked out for you.
- **Every plant gets its own ID** (GB-0001, GB-0002, …), a strain from a
  catalog you build up over time, and its own history and photos.
- **Charts of the environment**: temperature, humidity, VPD, PPM and, from a
  controller, CO₂, with the daily high and low.
- **Knows when you flipped the lights.** With a light sensor, 15 or more
  hours a day reads as veg and anything less as flower. Flip the timer and
  forget to tell the app, and the grow page notices and offers to record the
  flower date.
- **Smart outlets.** Shelly and Tasmota plugs pair straight to the app:
  switch them, see their power use, and save schedules into the plug itself,
  so they keep running with your computer off.
- **Home Assistant**: sensors and running grows appear there by themselves.
- **Your phone, if you want it.** Off by default. Turn it on, set an access
  code, and use GrowCircuit from your phone or tablet on your own Wi-Fi,
  photos from the phone's camera included.
- **Backup and restore in one file**, which you can protect with a password.

## Privacy

GrowCircuit has no account and no cloud. Your grows, plants, notes, photos
and sensor readings are stored only on the computer you install it on. We
never receive them, so we cannot see them, lose them or hand them over.

- **Photos lose their location.** Phones put GPS coordinates, the time and
  the handset inside every photo. GrowCircuit takes all of that out as a
  photo is added.
- **One outside connection**: a daily check for a new version, to this
  repository. It carries nothing about your grows, and it can be switched
  off in Settings.
- **Backups can be password-protected**, so a copy that ends up in a synced
  folder or on a USB stick gives nothing away.
- The app window clears its browser cache when it closes, and pages and
  photos are never cached by any browser, phones included.

## Sensors and controllers

GrowCircuit has its own sensor broker built in (MQTT, port 1883), so there is
nothing else to install. GrowCircuit sensors and controllers set themselves
up over Wi-Fi, appear in **Settings › Sensors** the first time they report,
and are assigned to a grow or a room from there. Their firmware updates are
signed and installed over the air from the app. **Settings › Diagnostics**
shows the raw traffic and a live sensor console for when something does not
show up.

Other devices can report too. Anything that can publish a small JSON message
over MQTT works, for example:

```json
{ "temp_c": 24.6, "humidity": 55.2, "light_on": true, "ppm": 840 }
```

## Installing

1. Download `GrowCircuit-<version>-x64.msi` from the
   [latest release](https://github.com/awarwick-mscst/GrowCircuit-releases/releases/latest).
2. Run it, accept the [licence](LICENSE) when asked, and approve the
   Windows administrator prompt. The app itself runs without administrator
   rights.
3. Open GrowCircuit from the Start Menu.

**Requirements:** Windows 10 version 1809 or later, or Windows 11, 64-bit,
and the Microsoft Edge WebView2 runtime, which Windows 11 and any recent
Windows 10 already have. The installer checks for it. Nothing else: no .NET
install, no database server, no separate MQTT broker.

### Is the download genuine?

Every installer is **code-signed by Aaron Warwick** through Microsoft's
Artifact Signing. Right-click the `.msi`, choose **Properties › Digital
Signatures**, and that name should be the signer.

A brand-new release can still meet a SmartScreen "Windows protected your PC"
warning for a while, because Microsoft judges files by how many people have
downloaded them. If the publisher shows as Aaron Warwick, choose **More info
› Run anyway**.

Every release also has a `.sha256` file beside the installer. To check a
download in PowerShell:

```powershell
Get-FileHash .\GrowCircuit-1.11.1-x64.msi -Algorithm SHA256
```

The hash must match the one in the `.sha256` file.

## Updating

GrowCircuit checks for a new version once a day and shows a banner when
there is one. Choose **Install** and it downloads the installer, refuses to
run it unless it is signed by Aaron Warwick, and upgrades in place. Your
grows, photos and settings are untouched.

Coming from version 1.6.0 or earlier? Those versions cannot install updates
by themselves. Download and run the newest installer once; later updates
install automatically.

## Your data

Everything GrowCircuit knows lives in one folder:

```
%LOCALAPPDATA%\GrowCircuit\
    growcircuit.db     the database
    photos\            every photo you have added
```

**Settings › Your data** makes a single backup file of all of it, and
restores one. If you set GrowCircuit up to run as a Windows service (so it
records from the moment the computer starts, with nobody signed in), the
folder moves to `%ProgramData%\GrowCircuit`, readable only by the service
and administrators.

## Licence

GrowCircuit is **proprietary software. Copyright © 2026 Aaron Warwick, all
rights reserved.** It is free to download, install and use, for your own
grows or your business. It may not be copied, modified, decompiled, reverse
engineered, redistributed or used to build a competing product. The full
terms are in [LICENSE](LICENSE) and [DISCLAIMER.md](DISCLAIMER.md), and by
installing or using GrowCircuit you accept them.

GrowCircuit is provided as is, without warranty of any kind. It is general
information and record-keeping software, not legal, medical or electrical
advice, and not a safety device. Making sure your grow is legal where you
live is your responsibility.

## Problems and questions

Open an [issue](https://github.com/awarwick-mscst/GrowCircuit-releases/issues)
in this repository. If a sensor is not showing up, **Settings › Diagnostics**
in the app is the first place to look, and its output is the most useful
thing to include.
