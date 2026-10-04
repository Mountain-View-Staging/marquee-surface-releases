# Marquee Surface releases

Signed installers for the Marquee Surface players, and nothing else: no source code, no settings, no
credentials. The players' in-app updaters read this repository's releases without a token, which is why it
is public.

## One repository, several players

Each player has its own **tag prefix**. An updater looks only at releases whose tag starts with its own
prefix, takes the newest version among them, and ignores everything else, so the players never pick up one
another's releases.

| Player | Tag | Installer asset |
|---|---|---|
| Windows (MarqueeSurfaceWin) | `windows-v<version>`, e.g. `windows-v0.5.0` | `MarqueeSurface-<version>-win-x64-setup.exe` |

Other players add a row here before their first release.

## What a release must be

- **Signed** with the Mountain View Staging code-signing certificate the player pins. A player refuses an
  installer that is unsigned, signed by anyone else, or altered after signing.
- **Exactly the file the build produced.** GitHub records each asset's SHA-256, and the player checks the
  download against it.
- **Not a draft and not a pre-release**, when it is meant for signs. Updaters skip both.
- **A version higher than the one before.** A player never installs an equal or lower version.

## Publishing

Build and sign with the player's own script (Windows: `tools/Build-Installer.ps1` in MarqueeSurfaceWin), then
create a release with the tag above and attach the installer. Signs on automatic updates install it in their
venue's night window, 04:00–05:00. Signs on manual updates install it when someone presses "Check now".

Never publish a Windows installer to the legacy player's repository (`Credmed1a/marquee-player-win`), and
never publish a legacy installer here.
