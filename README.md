httopd - top for httpd logs
====================================

[verdverm/httpod](https://github.com/verdverm/httpod)
pronounced "hopped" like a gopher

Dependencies
------------

1. Docker
2. *nix

Installation
-------------
`go get github.com/verdverm/httopd/httopd`

Running
-----------
`httopd -fn="/abs/path/to/log/file"`


Running Simulator
------------

1. `git clone https://github.com/verdverm/httopd && cd httopd`
2. `sudo build.sh`
3. `sudo run.sh`

   `sudo` is required for the docker commands (unless you run a non-sudo docker setup)

Enhancements / Issues / Todo's
------------------------------

Want to help out? Add or remove items from the following list.

- monitor multiple log files when there are multiple sites / server blocks
- there are race conditions on the statistics
  - there is a single reader and a single writer
  - shouldn't be too much of an issues since only one party reads and only one party writes
- page stats only update when new line_data shows up for that page
- add history and alerts to errors
- backfill with 10 minutes of history on startup
- sort by columns
- config file or directory inspection for log files / log directories
- ML triggers & alerts
- more configurable triggers / set from CLI / save to file?
- better log line parser
  - simpler and more flexible
  - only tested with nginx, need to check apache and others


Subdir Details
------------

#### server

This docker contains a Python-Flask site.

#### client

This docker contains a http-client simulator.

#### httpod

This docker contains the httpod program.

#### logs

a temporary directory created and destroyed by the simulator

References
---------------

1. [Logging Control In W3C httpd - Logfile Format](http://www.w3.org/Daemon/User/Config/Logging.html#common-logfile-format)
2. [termbox-go](https://github.com/nsf/termbox-go)
