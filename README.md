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

**With the app (easiest):** unzip `AeonTV-One-v2.0.0.zip`, open the
folder, run **AeonTV**. It starts everything in the background and
opens your station. Closing the window doesn't stop it — the
⏻ Stop button in the app is the off switch.

**Without the app:** unzip `AeonTV-One-folder-v2.0.0.zip`, then:

```bash
bash bin/start-aeontv.sh    # starts AeonTV One (port 8097)
bash bin/stop-aeontv.sh     # stops it
```

First start runs the setup wizard in your browser — make your admin
account and you're done. The live channel wires itself up.

## Included — officially tested

These public-domain classics from the Internet Archive were used to
test the channel scan end-to-end (scan → guide → live stream →
playback) and ship inside the program as your starter channel:

- **His Girl Friday (1940)**
- **House on Haunted Hill (1959)**
- **Reefer Madness (1938)**

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
