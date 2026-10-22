# AeonTV + ErsatzTV — the merged build

One package containing:

- **AeonTV** (the PS1-edition server build: Jellyfin 10.10.7
  rebrand with the AeonPS1 plugin bundled in) — watch on
  <http://localhost:8097>
- **ErsatzTV Legacy v26.11.3** (stock upstream) — the channel
  engine that turns your videos into always-on live TV
  channels with a program guide — <http://localhost:8409>

and a launcher that runs them together as one thing.

## The AppImage

`AeonTV-x86_64.AppImage` is the whole build in one file.

**First run asks where to install.** Pick a folder and it
copies itself there as `AeonTV.AppImage`, creates a `data/`
folder beside it (everything — both servers' data, your
channels, your media — lives in that one folder), and adds an
"AeonTV" entry to your app menu. Move or delete that one
folder and the whole install moves with it. Nothing else is
written outside it except the menu entry itself
(`~/.local/share/applications/aeontv.desktop`).

Choose **"Just run it"** instead and it runs portably; data
then lives in `~/.local/share/aeontv-livetv`.

Scripted install (no prompts):
`AEONTV_INSTALL_TO=/some/folder ./AeonTV-x86_64.AppImage`

If the AppImage won't start because your system lacks FUSE,
install `libfuse2` (Mint/Ubuntu: `sudo apt install libfuse2t64`
or `libfuse2`), or run it once with
`./AeonTV-x86_64.AppImage --appimage-extract` and start the
`AppRun` inside the extracted folder.

## Starting it

Double-click the AppImage (or the **AeonTV** menu entry once installed).
Starting is *visible*: your browser opens at <http://localhost:8097>
as soon as the servers are ready, and on a desktop a small
"AeonTV is running" window stays up — its **Stop AeonTV** button
shuts both servers down (there's also a **Stop AeonTV** menu entry
and `stop-aeontv.sh` next to the installed AppImage).

**The first start takes a few minutes** — ErsatzTV's database,
the channel and the guide are being built. Later starts are fast.
If truly nothing answers at <http://localhost:8097> after ~5
minutes, run it once from a terminal to see what's happening:
`./AeonTV-x86_64.AppImage` and read the output.

## Running the folder build instead

`bin/start-aeontv.sh` from this folder does the same thing
without the AppImage (data in `~/.local/share/aeontv-livetv`,
or set `AEONTV_DATA=/path`).

## Your channel

On first start the package provisions ErsatzTV automatically:

- a library pointing at **`data/media/livetv/`**
- an **"AeonTV Mix"** collection with everything in it
- an all-day flood schedule on **channel 1**, renamed **AeonTV**

**Drop videos into `data/media/livetv/` and restart the
launcher — they join the channel.** The launcher re-syncs the
collection on every start and ErsatzTV rebuilds the guide.

More channels, fancier schedules (blocks, marathons, filler):
build them in ErsatzTV's own UI at <http://localhost:8409> —
it's made for exactly that.

## See the channel inside AeonTV (one-time)

So the channel also appears in AeonTV's own **Live TV** section
with its guide, register ErsatzTV once as a tuner (needs your
AeonTV admin login, kept in the environment only):

```
AEONTV_USER=<admin> AEONTV_PASSWORD=<password> bin/wire-livetv.sh
```

It adds the M3U tuner + XMLTV guide provider, refreshes the
guide, and verifies the channel is listed. Safe to re-run.

## Updating

- AeonPS1 and the other AeonTV plugins: Dashboard → Plugins →
  Catalog, as always (newer copies supersede the bundled one).
- ErsatzTV is pinned at v26.11.3 in this build (stock
  upstream, the same version as the Berk ISO's). A future
  merged build swaps the `ersatztv/` folder.

## Notes

- ErsatzTV may warn that the bundled ffmpeg "is not an
  ErsatzTV-ffmpeg build" — cosmetic; the bundled ffmpeg (from
  the AeonTV build) transcodes the channels fine.
- ErsatzTV's own REST API requires its login system in this
  version; that's why provisioning writes to its database
  directly while it's stopped (the launcher handles the
  stop/start dance).
- Ports: AeonTV 8097, ErsatzTV 8409, both on localhost by
  default. Your nginx/Tailscale Funnel setup from the Bodhi
  box fronts 8097 the same way as before.
