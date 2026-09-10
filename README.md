# casparcg-builds

Published builds of the CasparCG Client fork. **Releases only** — the source
lives in [casparcg-client](https://github.com/inkvolcano/casparcg-client).

### ➜ [Download the latest build](https://github.com/inkvolcano/casparcg-builds/releases/latest)

Nothing is in the file list above except this README. The builds are **release
assets**, not repository files — a 214 MB binary in the tree would make the
repository unclonable. Use the link.

## What each release carries

| | |
|---|---|
| `casparcg-client-vX.Y.Z-NNN-windows.zip` | the build |
| `SHA256SUMS.txt` | check the download against this before installing |
| `install-update.cmd` | for updating a client older than build 210 |
| `server-php.zip` | the relay and sheet cache, for a web host rather than a venue machine |

The tag is `vMAJOR.MINOR.REVISION-BUILD`, and **the build number is the part that
moves**. The version behind it has not changed in years while the build has gone
past two hundred, so `v2.3.1-218` is newer than `v2.3.1-209` and that trailing
number is the one to compare.

## Updating

**On build 210 or newer**, the client does it: **Help → Check for Updates**. It
asks this repository what is published, says whether it is newer than what you
are running, downloads it, and checks it against `SHA256SUMS.txt` before writing
anything. **Install and Restart** then closes the client, puts the build in
place, and starts it again, keeping the one it replaced.

Nothing is checked or installed unless you ask. There is no timer and no check at
startup — this is the program running the show, and the moment to replace it is
yours.

**On anything older**, which has no Install and Restart: use Check for Updates →
Download → Show Download, put `install-update.cmd` from the release into the
folder that opens, close the client, and run it. It works out the rest for
itself. Only needed once — after that the client can do it.

## Installing by hand

Two ways it goes wrong, both of which leave you running the old build with new
libraries around it, and neither of which announces itself:

- **The zip holds one folder** named for the build. Copy what is **inside** it
  over your installation, not the folder itself.
- **Close the client first.** Windows will not replace a running executable, so
  copying over a running client updates every library and silently skips the one
  file that decides the version.

## Verifying a download

```
certutil -hashfile casparcg-client-v2.3.1-218-windows.zip SHA256
```

Compare it with the line in `SHA256SUMS.txt`. The client does this for you on
every download and refuses anything that does not match, without writing it to
disk.

## server-php.zip

The relay and the sheet cache, for a web host — not for a venue machine. Only
needed if you want the estate view showing which venue holds which templates and
runs which build. Templates and updates work without it.

It ships with each build because the relay protocol moves with the client, so
pairing them is how you tell which relay goes with which. Deploy **every** file
in it, the dotfiles included: `.htaccess` and `.user.ini` decide whether it works
at all.
