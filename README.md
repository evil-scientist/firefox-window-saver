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
  If Firefox is running, ffwin waits for you to quit it (Ctrl+Shift+Q), then restores. The windows that
  were open come back as well.
- `urls`: opens each window's tabs from the command line in the running Firefox. Tab groups and
  pinned tabs are not recreated, because the Firefox command line only accepts URLs.

Without `--mode`, ffwin uses `session` when Firefox is closed. When Firefox is open, it uses `urls` if the
windows have no tab groups or pinned tabs; otherwise it asks whether to quit Firefox and use `session`.

The profile is found automatically (snap, Flatpak, or regular install); use `--profile DIR` to override.
