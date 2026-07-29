<div align="center">

<img src="assets/logo.png" alt="Okami Cam" width="300">

# Okami Cam — downloads and APT repository

**Turn your Android phone into a native Linux webcam, over Wi‑Fi.**

[**okamicam website →**](https://julia-eileen.github.io/okami-cam-releases/)

</div>

---

Discord, Teams, Meet, Zoom and OBS see an ordinary camera at `/dev/video10`.
No cable, no browser tab, nothing leaving your network — and **the phone's
screen can stay off** while it streams.

## Install

Adding the repository is the recommended route: `apt upgrade` keeps Okami Cam
current from then on, and every package is GPG-signed and verified by apt.

```bash
# 1. Trust the release signing key
curl -fsSL https://julia-eileen.github.io/okami-cam-releases/okami-cam.gpg \
  | sudo tee /usr/share/keyrings/okami-cam.gpg > /dev/null

# 2. Point apt at the repository
echo "deb [signed-by=/usr/share/keyrings/okami-cam.gpg] https://julia-eileen.github.io/okami-cam-releases/apt stable main" \
  | sudo tee /etc/apt/sources.list.d/okami-cam.list

# 3. Install
sudo apt update && sudo apt install okami-cam
```

Prefer a one-off download? Grab the `.deb` from
[Releases](https://github.com/julia-eileen/okami-cam-releases/releases/latest)
and install it with **apt**, not `dpkg`, so the dependencies resolve:

```bash
sudo apt install ./okami-cam_0.1.0_amd64.deb
```

You also need the Android app on your phone, on the same Wi‑Fi network. It is
not on Google Play yet.

### If you have Secure Boot enabled

The kernel will refuse to load an unsigned `v4l2loopback`, and DKMS does not
sign modules on its own. Okami Cam detects this and explains what is happening
— it will never disable Secure Boot and never asks for your MOK password.
Enrolling a MOK key is a one-time step you carry out yourself.

## Requirements

| Desktop | Phone |
| --- | --- |
| Linux x86‑64, Debian or Ubuntu | Android 7.0 or newer |
| `ffmpeg` 8+, `v4l2loopback` | Camera permission |
| Polkit (`pkexec`) | Same Wi‑Fi network as the computer |

## What is in this repository

Everything here is **generated** by the release pipeline in the (private)
source repository. Do not send pull requests against these files — they are
overwritten on every release.

| Path | What it is |
| --- | --- |
| `index.html`, `assets/` | The website, served by GitHub Pages |
| `okami-cam.gpg` | Public half of the release signing key |
| `apt/dists/stable/` | Signed repository indexes (`InRelease`, `Packages`) |
| `apt/pool/` | The `.deb` packages themselves |

## Bugs and questions

Open an [issue](https://github.com/julia-eileen/okami-cam-releases/issues).
This repository is the support channel — the source code lives in a private
repository, so there is nowhere else to file one.

Useful things to include: your distribution and version, the output of
`okami-cam doctor`, whether Secure Boot is on, and your phone model.

## Privacy

Okami Cam has no servers and collects nothing. Your camera goes from your phone to
your own computer on your own network, and nowhere else. Full policy:
[okami-cam privacy policy](https://julia-eileen.github.io/okami-cam-releases/privacy.html).

## License

Okami Cam is **proprietary software**. © 2026 Julia Eileen Schäfer, all rights
reserved. You may install and run it on hardware you own or control. Any other
use — copying, modifying, redistributing, bundling it into another product —
needs prior written permission, and permitted use must credit the author.

The third-party components it builds on (ffmpeg, v4l2loopback, Tauri, and
others) remain under their own licenses, held by their own authors.
