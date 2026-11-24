# Changelog

## 1.0.0

First release under the iDive name. iDive continues IBMi-RUNSQL (last release
2.0.7).

### Changed
- Product renamed to iDive for IBM i; the window title is "iDive for IBM i".
- Application, bundle, and download names are now IBMi-iDive.
- Auto Recall host copies are stored in the `iDive` folder of the IBM i home
  directory (`Last_iDive_Session.sql`).
- Saved connections, settings, history, and passwords are migrated from
  IBMi-RUNSQL on first launch.

### Refreshed builds, 24 November 2026
The macOS and Windows 1.0.0 downloads were rebuilt with these updates.

#### Added
- Admin > Jobs: Display Job shows the Current Job Date in the job's own date
  format; a new Job Library List command lists the job's libraries; pasting a
  `number/user/name` job ID into the Job filter fills the Job, User, and Number
  filters.
- Admin > OUTQ: Work with SPOOLED Files, Hold, and Release on the right-click
  menu, including multiple selected queues. Admin > JOBQ has Hold and Release.
- Spooled file viewer: typing `*ERR` or `*ERROR` in Search jumps through the
  errors of RPG, SQL RPG, CL, command definition, DDS, C, and C++ compiler
  listings.
- Live Filter boxes for the SQL/CL results and the Job Log.
- The Session Log shows a `Client:` line (version and platform) on every
  connect, and in connection failures.

#### Changed
- Spooled file viewer: Greenbar, Page layout, and Copy now sit on the
  navigation bar, the Search box starts focused, the Page box accepts `T` for
  top and `B` for bottom, and the window title bar follows the app's theme.
- The Spooled Files and Job Log filters use the same look as the other Live
  Filter boxes.
- The Session Log no longer mentions a JDBC driver.

#### Fixed
- Connecting to an IBM i where the English language library is not installed
  (remote command server return code 0106) no longer stops with "refused the
  session".
- Right-click menus in the Admin panels close when you click outside the app
  window.
