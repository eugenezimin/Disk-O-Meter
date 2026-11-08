# DiskoMeter

A small menu bar app that shows how much your Mac's internal SSD reads and writes each day, and which processes do the writing.

<p align="center">
  <img src="screenshots/usage-light.png" width="420" alt="The Usage tab for a week, with read and written totals, a per-day average and a bar chart of each day">
  <img src="screenshots/processes-light.png" width="420" alt="The Processes tab for the same week, listing kernel_task, swift-frontend, mds_stores, Xcode and Safari by bytes written">
</p>

Every write wears an SSD a little, and on most modern Macs the drive is built in and can't be swapped when it wears out, yet macOS never tells you how much your machine actually writes in a day. DiskoMeter keeps that record from the menu bar, where it shows what has been written today, and a click opens a popover with the day, week, month or any range of days you choose, together with the processes behind the numbers.

## What you get

The menu bar shows today's writes in three digits, such as `27.9 GB`, so a glance is enough to notice a day that is running hot. The Usage tab shows how much was read and written during the chosen period, with an average per day and a chart that has a bar for each day, or for each week or month when you pick a long custom range. The arrows step back through earlier weeks and months, and Today brings you back to the present.

The Processes tab answers the next question, which is who did it. It lists every process that read or wrote during the same period, the biggest writers first, and lets you filter the list by name and sort it by bytes written, bytes read, total I/O or name. It can also narrow the list to your own apps or to the system's background processes, such as Spotlight's `mds_stores` or Time Machine's `backupd`, which are often the busiest of all.

Both tabs follow the light or dark appearance you have chosen for macOS, as these month-long views in dark mode show.

<p align="center">
  <img src="screenshots/usage-dark.png" width="420" alt="The Usage tab in dark mode for a month, with a bar pair for every day">
  <img src="screenshots/processes-dark.png" width="420" alt="The Processes tab in dark mode for the same month, with root processes tagged">
</p>

## Requirements

DiskoMeter needs macOS 26 or later on a Mac with Apple silicon.

## Download

The current version is 1.1.0, and the [release notes](RELEASE_NOTES.md) describe what each version brings. Download the disk image, which is the easiest way to install, or the ZIP archive, which holds the same app.

- [DiskoMeter.dmg](https://github.com/eugenezimin/Disk-O-Meter/raw/main/downloads/DiskoMeter.dmg) (328 KB, SHA-256 `00bfe8eb85c5ed35762497241d8d07d6648764c7319041e27119466ecc86b6d9`)
- [DiskoMeter.zip](https://github.com/eugenezimin/Disk-O-Meter/raw/main/downloads/DiskoMeter.zip) (283 KB, SHA-256 `94612dbd5de74a02032b2e64b8dbf85e845a20051433bdb8e0fd95c5dec0d325`)

## Installing

1. Open `DiskoMeter.dmg` and drag DiskoMeter onto the Applications folder beside it. If you downloaded the ZIP instead, double-click it and move the unpacked `DiskoMeter.app` into `/Applications`.
2. Open DiskoMeter from the Applications folder. The app is free and isn't notarized by Apple, so the first launch is stopped with a message that Apple could not verify it.
3. Open System Settings, go to Privacy & Security, scroll down to the note about DiskoMeter and click Open Anyway, then confirm with your password or Touch ID. macOS remembers the choice, so this happens only once.
4. Look for the drive icon in the menu bar and click it. To have DiskoMeter start with your Mac, turn on Launch at login at the bottom of the popover.

If you prefer the terminal, `xattr -dr com.apple.quarantine /Applications/DiskoMeter.app` removes the download flag and lets the app open straight away, in place of steps 2 and 3.

Because DiskoMeter can only count from the moment it first runs, the first day is a partial one, and the history grows from there.

## Seeing system processes

macOS lets an ordinary app read the disk counters of your own processes only, which leaves out the system's background services, and those often write the most. To see them, turn on Full process visibility at the bottom of the popover, or click Enable Full Visibility on the Processes tab. DiskoMeter then installs a small helper that runs in the background with administrator rights, and macOS asks you to approve it under System Settings › General › Login Items & Extensions. The helper only reads the per-process counters, which are process names and byte counts, and hands them to DiskoMeter. It writes nothing and answers only programs signed with DiskoMeter's identifier, and turning the switch off removes it again.

## Your data

Everything DiskoMeter records stays on your Mac, because the app makes no network connections and keeps its records in `~/Library/Application Support/DiskoMeter` as small JSON files, one for the daily totals and one per day for the processes.

## What the numbers mean

The figures are what the Mac sends to and fetches from the SSD, so they include everything that touches the drive, from apps and swap to Spotlight indexing, local Time Machine snapshots and system updates. They aren't the amount written to the flash chips inside the drive, which is usually somewhat higher and which Apple's SSDs don't report.

The process list can't account for every byte, because a process that starts and quits within a few seconds may never be seen, some writes are made by the system on a process's behalf, and the per-process counters include external drives as well. That is why the list ends with an Other / unattributed row, and why its total may differ from the SSD's.

## Removing DiskoMeter

First turn off Full process visibility and Launch at login in the popover, so neither the helper nor the login item is left behind. Then quit the app, move `DiskoMeter.app` from Applications to the Trash, and, if you don't want to keep the history, delete `~/Library/Application Support/DiskoMeter`.

## License

DiskoMeter is free to use and is released under the [MIT License](LICENSE). Copyright © 2026 Eugene Zimin. This repository holds the released app and its documentation, while the source code is kept private.
