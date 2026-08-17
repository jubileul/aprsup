# aprsup

Published firmware for the **Multi-APRS** station.

## What Multi-APRS is

A complete APRS station on one ESP32 board, connected to any VHF radio through
audio and PTT. It performs **three roles, each switching on and off on its own**
— the same station can be all three at once:

| Role | What it does |
| --- | --- |
| **Tracker** | Transmits its own position, from GPS or a fixed location, with smart beaconing that speeds up while moving and spares the channel while parked |
| **Digipeater** | Repeats packets from stations that cannot reach their destination alone, with hop control and protection against repeating the same packet twice |
| **iGate** | Carries what it hears on the air to the internet (APRS-IS), and can bring messages back from the internet to RF |

It receives and decodes AFSK 1200 baud, AX.25 and Mic-E — including position,
course, speed and symbol of whoever is transmitting.

**Everything is configured from a browser**, on a page that lives inside the
board itself: no app, no cable after the first flash, no configuration file. It
creates its own Wi-Fi network the first time, then joins the house network. The
page speaks **English and Portuguese**, and includes a map of the stations heard,
a packet log, and audio adjustment tools.

Once it is on the internet, **the board updates itself** — which is what this
repository is for.

---

## This repository

Holds **artifacts only**. The source code lives elsewhere and is private.
Stations in the field read the `latest.json` here on their own and update when a
new version is published.

| File | What it is |
| --- | --- |
| `latest.json` | Manifest: current version, address, size, SHA-256 and signature |
| `firmware-X.Y.Z.bin` | The image itself |

## Why this is public when the source is not

Because there is nothing to hide here. The binary is **already** flashed onto
every user's board, and it comes back out through the same USB cable that put it
there — publishing it reveals nothing that anyone holding a board does not
already have.

The alternative would be for the board to authenticate against a private
repository, which would require a token embedded in the firmware. An embedded
token is a public token, for the same reason: ESP32 memory is read with the cable
that writes it. And that token would grant read access to the entire source. Two
separate repositories trade an exposure that costs nothing for one that would
cost everything.

## Nothing here is trusted for being here

Every image is signed with ECDSA P-256, and the matching public key is built into
each board's firmware. The board **recomputes the image's SHA-256 as it writes**
and checks the signature before treating the new version as good. A swapped,
tampered or third-party image is refused, and the station carries on running the
version it already had.

That is why this repository being public is not a risk: it does not need to be
trusted for the mechanism to be safe.

## If you came here looking for the program to flash

This is not that file. There is an installer that does everything over USB, and a
manual with step-by-step instructions.

## Interested?

If the Multi-APRS station is of interest to you, get in touch:

**pp5eal.dev@gmail.com**
