# YouTube Music Lite for Omarchy

A free YouTube Music player for the Omarchy bar. It uses `ytmusicapi` for
library/search actions and MPV with `yt-dlp` for audio playback.

## Features

- Browser-cookie login with a manual-header fallback
- Search while typing
- Playlist browsing with explicit playlist playback
- Create private playlists from the player
- Play, pause, previous, next, shuffle, like, and dislike controls
- Remove tracks from playlists with right-click
- Album artwork and progress display
- Private per-user runtime state and MPV IPC socket

## Requirements

- Omarchy with the Quickshell bar
- Python 3
- MPV
- `yt-dlp`
- A Chromium-based browser or Firefox logged into YouTube Music

## Install

```bash
git clone https://github.com/stevenwtlafrance-ship-it/YouTube-Music-Lite.git
cd YouTube-Music-Lite
./install.sh
```

The installer creates a private virtual environment under
`~/.local/share/yt-music`, installs the exact hash-verified Python dependency
lock, installs the bar plugin, and enables it in the Omarchy bar. The installer
does not upgrade pip or download unpinned dependencies.

If you added the plugin with `omarchy plugin add`, run `./install.sh` from
`~/.config/omarchy/plugins/yt-music` to install the backend.

Log in after installation:

```bash
yt-music-ctl login
```

Click the music widget in the bar to open the player.

## Uninstall

```bash
./install.sh --uninstall
```

This removes the plugin, launcher, and virtual environment. Authentication
data under `~/.config/yt-music` is left untouched so it can be removed or
reused separately.

## Privacy

Authentication headers are stored locally in `~/.config/yt-music/auth.json`
with owner-only permissions. No credentials, playlists, or playback state
are included in this repository.

Browser cookies are not only read at login. If the saved session stops
validating, any player action that needs your account re-reads the YouTube
cookies from your Chromium-based browser (or Firefox) and overwrites
`auth.json` with them. To stop this, delete `~/.config/yt-music/auth.json`;
also sign out of YouTube in the browser if you don't want a later
`yt-music-ctl login` to pick the session up again.

## License

MIT. See [LICENSE](LICENSE).
