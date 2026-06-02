Watch the most recent GitHub Actions build for the current branch, wait for it to complete, then download and unzip the firmware artifacts to ~/Downloads/zmk-flash.

Steps:
1. Run `gh run list --branch $(git rev-parse --abbrev-ref HEAD) --limit 1 --json databaseId,status,conclusion,displayTitle` to get the latest run ID and status for the current branch.
2. If the run is `in_progress` or `queued`, run `gh run watch <id>` (with a 5 minute timeout) to wait for completion.
3. Check the final conclusion. If it is not `success`, report the failure and stop.
4. Remove any previous download: `rm -rf ~/Downloads/zmk-flash`
5. Download artifacts: `gh run download <id> --dir ~/Downloads/zmk-flash`
6. Unzip any zip files: `find ~/Downloads/zmk-flash -name "*.zip" -exec unzip -o {} -d ~/Downloads/zmk-flash/firmware \;`
7. List all `.uf2` files and print them with a short flashing guide:
   - Flash `keyball44_right` first (trackball side) — double-click reset on nice_nano to enter bootloader, drag `.uf2` to the mounted drive.
   - Then flash `keyball44_left`.
   - `settings_reset` is only needed to wipe BLE pairing.
