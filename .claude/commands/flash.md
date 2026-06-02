Watch the most recent GitHub Actions build for the current branch, wait for it to complete, download the firmware, then flash left and right halves automatically by waiting for the NICENANO bootloader volume.

Steps:
1. Run `gh run list --branch $(git rev-parse --abbrev-ref HEAD) --limit 1 --json databaseId,status,conclusion,displayTitle` to get the latest run ID and status for the current branch.
2. If the run is `in_progress` or `queued`, run `gh run watch <id>` (with a 5 minute timeout) to wait for completion.
3. Check the final conclusion. If it is not `success`, report the failure and stop.
4. Remove any previous download: `rm -rf ~/Downloads/zmk-flash`
5. Download artifacts: `gh run download <id> --dir ~/Downloads/zmk-flash`
6. Unzip any zip files: `find ~/Downloads/zmk-flash -name "*.zip" -exec unzip -o {} -d ~/Downloads/zmk-flash/firmware \;`
7. Find the left and right .uf2 file paths:
   - LEFT: the file matching `*keyball44_left*.uf2`
   - RIGHT: the file matching `*keyball44_right*.uf2`
8. Flash left half:
   - Tell the user: "Double-click reset on the LEFT half to enter bootloader mode."
   - Wait for /Volumes/NICENANO to appear: `until [ -d /Volumes/NICENANO ]; do sleep 1; done`
   - Copy the left .uf2: `cp "<left_uf2>" /Volumes/NICENANO/`
   - Tell the user the left half is flashed and wait for the volume to disappear: `while [ -d /Volumes/NICENANO ]; do sleep 1; done`
9. Flash right half:
   - Tell the user: "Double-click reset on the RIGHT half to enter bootloader mode."
   - Wait for /Volumes/NICENANO to appear: `until [ -d /Volumes/NICENANO ]; do sleep 1; done`
   - Copy the right .uf2: `cp "<right_uf2>" /Volumes/NICENANO/`
   - Tell the user the right half is flashed and wait for the volume to disappear: `while [ -d /Volumes/NICENANO ]; do sleep 1; done`
10. Report success: both halves flashed. Remind the user that `settings_reset-nice_nano_v2-zmk.uf2` is available in ~/Downloads/zmk-flash/firmware/ if they need to wipe BLE pairing.
