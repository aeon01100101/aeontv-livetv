# AeonTV One

**One program.** AeonTV (your movie & show server) with the live-channel
engine and the PS1 game shelf built *into* it. No second program, no
side server — one process, one port, one home screen.

- **Watch** — your library, at `http://localhost:8097`
- **Live Channels** (AeonLive, built in) — folders of videos become
  always-on TV channels with a real program guide inside AeonTV's
  Live TV section. Shuffle or in-order, always in sync for everyone.
- **PS1 Games** (AeonPS1, built in) — a games folder becomes a shelf
  with real serials read off the discs and cover art; play in the
  browser or on the Fire TV app.

## Run it

Downloads are on the
[releases page](https://github.com/aeon01100101/aeontv-livetv/releases) —
the program zip plus the starter movies in three small packs.
Windows and Linux builds are both there.

**Windows — with the app (easiest):** unzip
`AeonTV-One-App-Win-v2.0.0.zip`, open the folder, run **AeonTV.exe**.
It starts everything in the background and opens your station.
Closing the window doesn't stop it — the ⏻ Stop button in the app
is the off switch. (Unsigned: SmartScreen may warn once — More info
→ Run anyway.)

**Windows — without the app:** unzip `AeonTV-One-Folder-Win-v2.0.0.zip`
and double-click `bin\start-aeontv.bat` (Ctrl+C stops it;
`bin\stop-aeontv.bat` stops it from another window).

**Linux — with the app:** unzip `AeonTV-One-App-v2.0.0.zip`, open
the folder, run **AeonTV**. Same deal: background start, the
⏻ Stop button is the off switch.

**Linux — without the app:** unzip `AeonTV-One-Folder-v2.0.0.zip`, then:

```bash
bash bin/start-aeontv.sh    # starts AeonTV One (port 8097)
bash bin/stop-aeontv.sh     # stops it
```

First start runs the setup wizard in your browser — make your admin
account and you're done. The live channel wires itself up.

## Starter movies — officially tested

These public-domain classics from the Internet Archive were used to
test the channel scan end-to-end (scan → guide → live stream →
playback). Each is its own download pack; unzip it and drop the
`media` folder into the program folder so the movie lands in
`media/livetv` (for the app: into `AeonTV-One/resources/payload`),
before the first start:

- **AeonTV-One-Starter-Movies-A-v2.0.0.zip** — His Girl Friday (1940)
- **AeonTV-One-Starter-Movies-B-v2.0.0.zip** — House on Haunted Hill (1959)
- **AeonTV-One-Starter-Movies-C-v2.0.0.zip** — Reefer Madness (1938)

## Add your own

- **Videos → live channel:** drop files into the `media/livetv`
  folder in AeonTV's data folder (the app's ➕ Add Videos button
  opens it), then open **Live Channels** in AeonTV and press
  **Rescan**. Name files like `Title (Year).mp4` and the guide
  shows them properly. More folders = more channels (Live Channels
  → Add channel).
- **PS1 games:** in AeonTV open **AeonPS1** settings and point it at
  your games folder (.bin/.cue/.iso/.img/.pbp/.chd). A .bin + .cue
  pair counts as one game. For browser play, drop your PS1 BIOS
  (`scph*.bin`) into the same folder — without it, games run on the
  emulator's built-in BIOS and some won't boot right.

## Notes

- Data lives beside the app in `data/` (or `$AEONTV_DATA`). Your
  library, accounts and channels survive updates — replace the
  program folder, keep `data/`.
- Port: **8097** (change with `AEONTV_PORT`).
- Linux x86-64. Needs `libfuse2` for *nothing* — there is no
  AppImage anymore; it's a plain folder.
