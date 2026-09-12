🌱 GrowCircuit
A grow room monitor and grow journal for Windows that keeps everything on your own computer.

GrowCircuit tracks indoor grows from veg through flower to harvest, and — with a sensor in the room — records what the environment was doing the whole time. It is built for people growing high-value crops where a missed light flip, a humidity spike or a drifting nutrient mix costs real money.

This repository holds the installers. Download the newest one from ../../releases.

What it does
Keeps the record. Run as many grows as you like at once. Each grow has a veg start, a flower start and a harvest date, and the app works out the phase and the day count from those — set the date, and "day 39 of flower" follows. Every plant gets its own ID (GB-0001, GB-0002, …), a strain from a catalog you build up over time, and an optional label of your own. Attach timestamped notes and photos to the grow or to an individual plant.

Watches the room. Point a sensor at the space and GrowCircuit logs temperature, humidity, light level, whether the light is on, and nutrient strength (PPM) for hydroponic setups. The environment history is charted per day with the daily high/low band, so you see the room rather than a single instant.

Notices when you flipped the lights. A grow runs long days through veg and switches to 12/12 to trigger flowering. GrowCircuit reads that straight off the light sensor: 15 or more hours a day is a veg schedule, anything less is flowering. If you flip the timer and forget to update the app, the grow page says so and offers to record the flower start date for you. It only judges complete days and averages a few of them, so opening the tent at night is not mistaken for a phase change.

Stays on your machine. The database and your photos live in one folder under your Windows profile. Nothing about your grows, plants or readings is ever sent anywhere. The only request the app makes off your computer is a once-a-day check of this repository for a new version, and that can be switched off in Settings.

Backs up in one file. Export a single zip holding the database, every photo and the whole record as CSV. Restoring is staged and applied on the next start, and whatever it replaces is moved aside rather than deleted.

Reaches your phone, if you want it to. Off by default. Turn it on in Settings, set an access code, and the same interface is available on your phone or tablet over your own Wi-Fi — including taking plant photos from the phone's camera.

Is free. The app costs nothing and has no accounts, subscriptions or licence keys.

Sensors
GrowCircuit includes its own sensor broker (MQTT, port 1883), so there is nothing else to install or run. A sensor publishes a small JSON reading, registers itself the first time it does, and you assign it to a grow under Settings › Sensors.

The official hardware is an ESP32 board with a temperature/humidity sensor, a light sensor, and optionally a nutrient (TDS) probe. It sets itself up over a Wi-Fi captive portal, so there is no configuration file to edit and nothing to flash by hand. Sensor firmware updates are delivered through the app: Settings › Sensors shows an Update button when a newer signed image is available, and the sensor installs it over the air.

The protocol is deliberately open — any MQTT device that can publish a line like this will work:

{ "temp_c": 24.6, "humidity": 55.2, "light_on": true, "ppm": 840 }
Settings › Diagnostics shows the raw traffic the broker is seeing and a live console of the sensor's own log output, over USB or Wi-Fi, for when something is not showing up.

Installing
Download GrowCircuit-<version>-x64.msi from the newest entry under Releases.
Run it. Windows asks for administrator approval to install; the app itself runs without it.
Launch GrowCircuit from the Start Menu.
Requirements: Windows 10 version 1809 or later, or Windows 11, 64-bit. The app needs the Microsoft Edge WebView2 runtime, which is already on Windows 11 and any recent Windows 10; the installer checks and tells you if it is missing. Nothing else — no .NET install, no database server, no separate MQTT broker.

"Windows protected your PC"
These builds are not code-signed yet, so SmartScreen reports the publisher as unknown. Choose More info, then Run anyway. Some managed machines with strict Defender rules may refuse to run an unsigned installer at all; if yours does, your administrator will need to allow it.

Every release ships a .sha256 file beside the installer. To confirm the download is what we published, in PowerShell:

Get-FileHash .\GrowCircuit-1.3.1-x64.msi -Algorithm SHA256
and compare the hash with the contents of the .sha256 file.

Updating
GrowCircuit checks this repository once a day. When there is a newer version it shows a banner in the app. While the builds are unsigned the app will not install the update by itself — it refuses to run anything it cannot verify was built by us — so the banner links you back here to download and run the new installer. Installing over the top upgrades in place; your database and photos are untouched.

Your data
%LOCALAPPDATA%\GrowCircuit\
    growcircuit.db     the database
    photos\            every photo you have added
Backing up GrowCircuit is copying that folder, or using Settings › Your data to produce a single zip.

What is in this repository
Only release assets, on two kinds of tag:

Tag	What it is
v1.3.1	The Windows app: an .msi and its .sha256
fw-v1.4.0	Sensor firmware: signed images and a manifest, picked up by the app
You do not need to download firmware releases yourself — the app finds them and offers them to each sensor they apply to.

The source code is not published here.

Problems and questions
Open an issue in this repository. If a sensor is not showing up, the Settings › Diagnostics page in the app is the first place to look, and its output is the most useful thing to include.
