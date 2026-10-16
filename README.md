# Fluxplan Signage releases

SD card images and player updates for [Fluxplan](https://fluxplan.nl) screens on a Raspberry Pi 4 or 5.

## Getting started

1. Download the latest `fluxplan-signage-<version>.img.xz` from [Releases](../../releases).
2. Write it to a microSD card with [Raspberry Pi Imager](https://www.raspberrypi.com/software/) ("Use custom") or balenaEtcher. You can also add this repository to Raspberry Pi Imager: `rpi-imager --repo https://enjoytheshow-nl.github.io/fluxplan-signage-releases/imager.json`.
3. Put the card in the Pi, connect a TV, a network cable if you have one, and power. Then follow the instructions on the TV.

## Updates

Players install updates by themselves at night, from the signed apt repository at
`https://enjoytheshow-nl.github.io/fluxplan-signage-releases/apt` (key fingerprint `C57F858FA9B27EE98EA313EF5A39CD8F9F30CF35`).

This repository only holds published releases; it is updated automatically.
