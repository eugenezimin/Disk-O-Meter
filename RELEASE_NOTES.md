# DiskoMeter release notes

## 1.2.0, November 8, 2026

DiskoMeter 1.2.0 is the first version signed with a Developer ID and notarized by Apple, so it opens like any other app, without the detour through Privacy & Security that earlier versions needed. It also reaches beyond the internal SSD to your external disks, charts a single day hour by hour, and gathers its switches on a tab of their own.

The Usage tab now opens with a menu that chooses the disk. The internal SSD is the default, and every external disk on USB or Thunderbolt keeps a history of its own from the moment DiskoMeter first sees it. The app recognizes a disk by its serial number, so the history follows it from one port or one session to the next, and a disk you have unplugged stays in the menu, so you can still look back at what it read and wrote. Cards in the built-in SD reader and mounted disk images are left out.

When the period is a single day, whether you pick Day or a one-day custom range, the chart now shows a pair of bars for every hour, which makes it easy to see when the heavy writing happened, and its scale switches to megabytes on a quiet day. Weeks and months keep a pair of bars per day. Hourly figures are kept from this version on, so a day from before the update shows its totals with a short note in place of the bars.

A new Settings tab beside Usage and Processes holds Launch at login, Full process visibility, the About button with the version, and Quit. While the helper waits for your approval, a note under its switch takes you straight to the right page of System Settings. The disk name above the tabs and the line of boot-time totals below them are gone, which leaves the popover a little shorter and the same height on every tab.

Your history carries over, and to be safe, turn off Full process visibility before you replace an earlier version and turn it back on afterwards. The helper is now signed together with the app and only answers a DiskoMeter signed by the same developer, and because its signature changes with this release, macOS may ask you to approve it again in System Settings › General › Login Items & Extensions.

## 1.1.1, November 8, 2026

DiskoMeter now has its own icon, a gauge whose arc runs from the app's read blue through violet to its write red on a dark tile, which replaces the generic app icon in Finder, in the About panel and in the Login Items list of System Settings. Nothing else changes, and an installed 1.1.0 can simply be replaced with this version.

## 1.1.0, November 8, 2026

This is the first public release of DiskoMeter, a menu bar app for macOS 26 and later on Apple silicon that records how much your Mac's internal SSD reads and writes each day and shows which processes do the writing.

The menu bar shows today's writes in exactly three digits, such as `27.9 GB` or `3.46 GB`, so a single glance tells you whether the day is quiet or running hot. A click opens a popover with two tabs that share one period, which can be a day, a calendar week, a calendar month or any custom range of days. The arrows step back through earlier periods without ever running past today, and Today returns you to the present.

The Usage tab shows how much was read and written during the period, with an average per day for anything longer than a day and the live rate whenever the period includes today. Its chart draws a pair of bars for each day, and it groups a long custom range into weeks, or into months beyond a year, so the bars stay readable. Reads are blue and writes are red throughout, in colors chosen to stay distinct for color-blind readers in both light and dark mode.

The Processes tab lists every process that read or wrote during the same period, the biggest writers first. A search field narrows the list by name, and the menu beside it sorts by bytes written, bytes read, total I/O or name, in either direction, and can limit the list to your own apps or to the system's background processes, a sort and a choice that DiskoMeter remembers between launches. A final Other / unattributed row shows the writes that no sampled process accounts for, so the list never pretends to explain more than it can.

Because macOS lets an ordinary app read only your own processes, the busiest writers, such as Spotlight's `mds_stores` and Time Machine's `backupd`, stay hidden until you turn on Full process visibility. DiskoMeter then installs a small helper that runs with administrator rights after you approve it in System Settings › General › Login Items & Extensions. The helper only reads process names and byte counts and writes nothing, and switching it off removes it again.

Everything DiskoMeter records stays on your Mac, because the app makes no network connections and keeps its records as small JSON files in `~/Library/Application Support/DiskoMeter`, saving them every few minutes and whenever the app quits or the Mac sleeps or shuts down, so a relaunch carries on where the last session stopped. The About DiskoMeter button in the popover shows the version and the copyright notice, and Launch at login starts the app with your Mac.

A few limits come with the approach, the first being that counting begins when the app first runs, so the first day is a partial one. A process that starts and quits within a few seconds may never be seen, and the per-process figures include external drives, which is why they may not add up to the SSD's total. The app is signed ad hoc rather than notarized by Apple, so the first launch needs Open Anyway in System Settings › Privacy & Security, as the [README](README.md#installing) explains.

Every version from 1.2.0 on can be downloaded from the [Releases](https://github.com/eugenezimin/Disk-O-Meter/releases) page.
