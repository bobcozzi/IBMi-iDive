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

### Refreshed builds, third update, 24 November 2026
The macOS, Windows, and iPad 1.0.0 builds were rebuilt again with these updates.

#### Added
- Job Log window: a Refresh button reloads the job log. When the job has ended
  and its job log is gone, the window does not open (or closes on Refresh) and
  a brief message, "Job ended no joblog available", appears instead.
- Quit App setting (Settings > Application > Notifications): Never, Multiple
  Connections, or Always. The quit prompt has a "Never ask again" switch that
  sets it to Never; scripts are still saved before the app exits.
- Settings > Application: Theme and the Control Tabs Text and Background colors
  are grouped under Appearance/Theme.

#### Changed
- The Save/OK and Cancel buttons of the quit prompt respond reliably even when
  the mouse moves slightly while clicking.

#### Fixed
- Spooled file viewer: `*ERR` / `*ERROR` now recognizes SQL RPG precompiler
  listings (product IDs such as 5770ST1), finds the compiler banner anywhere in
  the first lines of the listing, and also flags the RPG compile errors in SQL
  RPG listings.

### Refreshed builds, second update, 24 November 2026
The macOS, Windows, and iPad 1.0.0 builds were rebuilt again with these updates.

#### Added
- Connections menu with Disconnect, Reconnect, and Load Script from Host. They
  act on the active connection.
- A failed SQL statement or CL command lists the job log messages (message ID,
  text, and the From/To program details) in the results.
- Closing the app with open connections offers to save your scripts first.
- A persistent app log (`iDive session log.txt`) and a Settings > Support page
  with buttons for the support folder, reporting an issue, and releases.
- Connections: an Add All button for the Admin Views list.

#### Changed
- Auto Recall with several connections to the same host and user: only the
  first connection saves its script to the IBM i host and loads it at connect
  (falling back to the local copy when the host has none). Additional
  connections never read or write the host; each keeps its own numbered local
  script (`..._Last_Session_2.sql`, `_3`, and so on) and starts empty when it
  has none. Use Connections > Load Script from Host to bring the saved host
  script into any connection on demand.
- A reconnect keeps its connection number.
- Local session files use underscores in place of dots in the host name
  (`10_0_0_21_USER_Last_Session.sql`); existing files are renamed on first use.
- The connection option "CL Processing" offers CL Job or SQL Job; the Return
  CL Messages switch is gone because messages are always returned.
- Admin default view order and titles: Active Jobs, Job Queues, Output Queues,
  Job Scheduler, Printers, QHST.
- All right-click menus share one implementation and one row-selection look.

#### Fixed
- Running with the caret after a statement's closing `;` no longer runs the
  previous statement.

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
