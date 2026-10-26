# SRUM Checker

SRUM Checker is an advanced Windows SRUM parser built for screenshare and forensic analysis.
It reads the `SRUDB.dat` database, where Windows keeps roughly 30 days of application activity, and turns it into a clean table showing proof of execution, even for files that were already deleted or renamed.

The project also includes:

* Fully automatic SRUDB parsing and CSV analysis
* Digital signature verification
* Path resolution for entries that only store the file name
* Duplicate grouping (one result per file)
* Built-in search box

## Features

### Automatic SRUDB Parsing

* One click does everything:
   * Downloads SrumECmd if it's missing
   * Parses `SRUDB.dat` and exports the CSV
   * Opens and analyzes `AppTimelineProvider_Output`
   * Cleans up temporary files when finished
* Already have the CSV? Open it manually.

### Path Resolution

* Automatically converts `\Device\HarddiskVolumeN\` device paths into standard drive-letter paths (`C:\`, `D:\`, etc).
* When SRUM only stores the file name (`firefox.exe`, `svchost.exe`), it finds the full path using:
   * The other SRUM tables
   * Running processes
   * System folders
   * A time-limited disk search

### Digital Signature Verification

* Verifies the digital signature of every file that still exists.
* Detects:
   * Unsigned files
   * Fake or tampered signatures
   * Untrusted signatures
* If the same name points to several paths, the suspicious one is the one shown.

### Duplicate Grouping

* The same file and path appears only once.
* Each result shows:
   * Last execution (local time and UTC)
   * Number of records
   * Users
* Selecting a row also reveals the first time it was seen.

### Search

* Built-in search box to filter by file name or path.
* Multiple words supported: every word must match.
* `Ctrl + F` to focus, `Esc` to clear.

Makes finding suspicious entries way easier.

### Filters

`Post Logon`
Shows all entries executed after the PC started.
The start time is detected automatically and can be edited by hand.

`Show Untrusted` (red)
Displays entries flagged as:

* Unsigned
* Fake or tampered signature
* Untrusted signature

`Show Not Found` (yellow)
Displays paths that were deleted, renamed, or couldn't be located on disk.

Filters can be combined and work together with the search box.
