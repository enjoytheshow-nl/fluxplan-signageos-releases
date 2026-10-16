# Fluxplan SignageOS

Fluxplan SignageOS turns a Raspberry Pi into a screen for [Fluxplan](https://fluxplan.nl). Connect it to a TV and set it up once with your phone. You don't need a keyboard, mouse or separate signage software. From then on, the screen shows the view you picked for it in the Fluxplan admin: the day's planning in the lobby, or a single room's schedule next to its door.

The screen looks after itself. It installs its own updates at night, picks up again after a power or network cut, and you can restart, update or reset it from the Fluxplan admin.

This repository publishes the SD card images and player updates.

## What you need

- A **Raspberry Pi 5 or 4** with its official power supply
- A **microSD card** of 8 GB or more
- A **TV or monitor** with HDMI, plus the right cable (micro-HDMI on the Pi)
- A **network**: Wi-Fi or a network cable
- A **Fluxplan** you can sign in to as an admin

## Installing a screen

1. **Download** the latest `fluxplan-signageos-<version>.img.xz` from [Releases](../../releases/latest).
2. **Write it to the microSD card** with [Raspberry Pi Imager](https://www.raspberrypi.com/software/) (*Choose OS → Use custom*) or [balenaEtcher](https://etcher.balena.io/). Leave Imager's "OS customisation" off: the screen sets itself up.
3. **Start the Pi.** Put the card in the Pi, then connect the TV, a network cable if you use one, and lastly the power.
4. **Set it up with your phone.** The TV shows the name and password of a temporary Wi-Fi network (`Fluxplan-SignageOS-…`) and a QR code. Join it, and the setup page opens by itself in Dutch or English (otherwise go to `http://10.42.0.1`). Choose Wi-Fi or a network cable, enter your Fluxplan address (for example `demo.fluxplan.nl`) and your country, then choose **Save and connect**.
5. **Pair it.** The TV shows a pairing code. In the Fluxplan admin, open **Narrowcasting**, choose **Pair screen** and enter the code. Then pick what the screen shows.

Once connected, the screen installs the newest version of the player right away. Within a minute of pairing, it shows its view.

The full guide, in Dutch, is in the Help section of your Fluxplan admin.

### Through Raspberry Pi Imager's own list

Raspberry Pi Imager can also list Fluxplan SignageOS directly, so you don't need to download the image first:

```
rpi-imager --repo https://enjoytheshow-nl.github.io/fluxplan-signageos-releases/imager.json
```

## Setting up in advance

If you know the Fluxplan address and Wi-Fi details beforehand, you can skip the phone step. After writing the card, open it on your computer and put a file called `fluxplan.json` next to `FLUXPLAN-README.txt`:

```json
{
    "server": "demo.fluxplan.nl",
    "country": "NL",
    "wifi": { "ssid": "Office", "password": "secret", "hidden": false }
}
```

Leave out `"wifi"` when the Pi uses a network cable. The screen reads the file on its first start, then deletes it, because the file contains your Wi-Fi password.

## Looking after a screen

**Automatically:** every night the screen installs Debian, Raspberry Pi and player updates, and restarts at 04:00 if an update needs it. It also restarts every Sunday night. If the page freezes or the board stops refreshing, the screen reloads it. If that doesn't help, it restarts the browser, and in the end the whole Pi.

**From the Fluxplan admin:** under **Narrowcasting**, each screen has a **Player** menu.

- **Update player:** install a new version now instead of tonight.
- **Restart:** restart the Pi.
- **Shut down:** turn the Pi off, for example before you move it. To start it again, unplug the power and plug it back in.
- **Factory reset:** the screen forgets your Fluxplan, its pairing and its Wi-Fi network, and goes back to setup.

**Without the admin:** if a screen is offline, you can also reset it from the SD card. Create an empty file called `fluxplan-reset` next to `FLUXPLAN-README.txt`, then put the card back in the Pi.

## Security

- The screen only ever opens its own Fluxplan, and only the views Fluxplan offers. Every other web address is blocked.
- Nobody can log in to the Pi: the account is locked and SSH is off. The firewall only allows what setup needs.
- Updates come from a signed apt repository at `https://enjoytheshow-nl.github.io/fluxplan-signageos-releases/apt`. The signing key's fingerprint is `C57F858FA9B27EE98EA313EF5A39CD8F9F30CF35`.
- Each release lists a SHA-256 checksum (`.img.xz.sha256`), so you can check your download.

## About this repository

Releases here are published automatically: there is no code to build. Each player version is published to the apt repository, where screens pick it up. A new SD card image is only published when the image itself changes. An older image is fine to use, because it updates itself to the newest player once it's connected.
