# DiskoMeter release notes

## 1.1.0, November 8, 2026

This is the first public release of DiskoMeter, a menu bar app for macOS 26 and later on Apple silicon that records how much your Mac's internal SSD reads and writes each day and shows which processes do the writing.

The menu bar shows today's writes in exactly three digits, such as `27.9 GB` or `3.46 GB`, so a single glance tells you whether the day is quiet or running hot. A click opens a popover with two tabs that share one period, which can be a day, a calendar week, a calendar month or any custom range of days. The arrows step back through earlier periods without ever running past today, and Today returns you to the present.

The Usage tab shows how much was read and written during the period, with an average per day for anything longer than a day and the live rate whenever the period includes today. Its chart draws a pair of bars for each day, and it groups a long custom range into weeks, or into months beyond a year, so the bars stay readable. Reads are blue and writes are red throughout, in colors chosen to stay distinct for color-blind readers in both light and dark mode.

The Processes tab lists every process that read or wrote during the same period, the biggest writers first. A search field narrows the list by name, and the menu beside it sorts by bytes written, bytes read, total I/O or name, in either direction, and can limit the list to your own apps or to the system's background processes, a sort and a choice that DiskoMeter remembers between launches. A final Other / unattributed row shows the writes that no sampled process accounts for, so the list never pretends to explain more than it can.

Because macOS lets an ordinary app read only your own processes, the busiest writers, such as Spotlight's `mds_stores` and Time Machine's `backupd`, stay hidden until you turn on Full process visibility. DiskoMeter then installs a small helper that runs with administrator rights after you approve it in System Settings › General › Login Items & Extensions. The helper only reads process names and byte counts and writes nothing, and switching it off removes it again.

Everything DiskoMeter records stays on your Mac, because the app makes no network connections and keeps its records as small JSON files in `~/Library/Application Support/DiskoMeter`, saving them every few minutes and whenever the app quits or the Mac sleeps or shuts down, so a relaunch carries on where the last session stopped. The About DiskoMeter button in the popover shows the version and the copyright notice, and Launch at login starts the app with your Mac.

A few limits come with the approach, the first being that counting begins when the app first runs, so the first day is a partial one. A process that starts and quits within a few seconds may never be seen, and the per-process figures include external drives, which is why they may not add up to the SSD's total. The app is signed ad hoc rather than notarized by Apple, so the first launch needs Open Anyway in System Settings › Privacy & Security, as the [README](README.md#installing) explains.

Download [DiskoMeter.dmg](https://github.com/eugenezimin/Disk-O-Meter/raw/main/downloads/DiskoMeter.dmg) or [DiskoMeter.zip](https://github.com/eugenezimin/Disk-O-Meter/raw/main/downloads/DiskoMeter.zip).
