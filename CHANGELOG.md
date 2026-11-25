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

### Refreshed builds, fourth update, 25 November 2026
The macOS, Windows, and iPad 1.0.0 builds were rebuilt again with these updates.

#### Added
- Admin > Active Jobs: right-click a job for Work with Job SPOOLED Files (opens
  the Spooled Files list filtered to that job) and Copy Job Name
  (`number/user/name`). A Qualified Job Name column is available in the column
  settings, and Current User is shown in bold when it differs from the job's
  user. Pasting a three-part job name into the Spooled Files Job Filter fills
  Name, User, and Number.
- Auto-refresh for Admin views and Message queues: a switch and an interval
  from 30 seconds to 30 minutes. It is off at every launch, refreshes without
  clearing your selection, pauses when you leave the panel and refreshes when
  you return, and turns itself off after a failed refresh.
- Kiosk (fullscreen) mode for Admin views and Message queues, from the
  full-screen button or View > Kiosk View. Only the list and a title bar are
  shown; Esc or Enter returns to the normal window. The title bar says when
  auto-refresh is disabled.
- Connections > Export / Import Connections and Settings to/from Host (also on
  the Settings > Export / Import page, which is how to use it on iPad). Your
  connections, settings, and statement history are saved in the `iDive` folder
  of your IBM i home directory so another device can load them. Saved
  passwords and local folder locations are not included.
- Messages: a Reset menu for sorting and column widths, and Remove for a
  message queue from its right-click menu (swipe it left on iPad). The queue
  list follows the Startup Message Queues you save under Connections, and
  `*USER` shows your assigned message queue name as soon as the panel loads.
- Admin > Job Queues: Active Jobs and Queued Jobs switches, off by default,
  show only queues with a count above 0.

#### Changed
- Job Queues columns: Jobs is now Queued Jobs and sits next to Active Jobs.
  The default order is Queue, Status, Queued Jobs, Active Jobs, Max Jobs,
  Subsystem, Seq, Description, and ASP; Subsystem Library is hidden by
  default. Saved column layouts are unchanged.
- Dialog buttons now put Cancel before the action throughout the app (for
  example Cancel | Save, Cancel | Remove).
- Removing a message queue from the list confirms with Remove, not Delete.
- New splash image.

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
