# firefox-window-saver

`ffwin` saves and restores Firefox windows, tabs and tab groups. It is one Python 3 script with no
dependencies and no browser extension.

It reads Firefox's own session file (`sessionstore-backups/recovery.jsonlz4`) and keeps snapshots as
JSON in `saves/` (or `$FFWIN_DIR`), outside the Firefox profile, so Firefox updates cannot wipe them.

```
ffwin windows                          # windows open now, with their tab groups
ffwin save [--all | --window N] [--name TEXT]
ffwin save --from FILE                 # read another session file, e.g. previous.jsonlz4
ffwin list | show [SNAPSHOT]
ffwin restore [SNAPSHOT] [--all | --window N] [--mode urls|session]
```

Restore modes:

- `session` (default when Firefox is closed): writes the windows into the profile's session file and
  starts Firefox. Keeps tab groups, pinned tabs and history. The current session file is backed up first.
- `urls` (default while Firefox is open): opens each window's tabs from the command line. Tab groups
  and pinned tabs are not recreated.

The profile is found automatically (snap, Flatpak, or regular install); use `--profile DIR` to override.
