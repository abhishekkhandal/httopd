我是光年实验室高级招聘经理。
我在github上访问了你的开源项目，你的代码超赞。你最近有没有在看工作机会，我们在招软件开发工程师，拉钩和BOSS等招聘网站也发布了相关岗位，有公司和职位的详细信息。
我们公司在杭州，业务主要做流量增长，是很多大型互联网公司的流量顾问。公司弹性工作制，福利齐全，发展潜力大，良好的办公环境和学习氛围。
公司官网是http://www.gnlab.com,公司地址是杭州市西湖区古墩路紫金广场B座，若你感兴趣，欢迎与我联系，
电话是0571-88839161，手机号：18668131388，微信号：echo 'bGhsaGxoMTEyNAo='|base64 -D ,静待佳音。如有打扰，还请见谅，祝生活愉快工作顺利。

httopd - top for httpd logs
====================================

pronounced "hopped" like a gopher

![boing!](https://raw.github.com/verdverm/httopd/master/glenda_space_medium.jpg)


Dependencies
------------

1. Docker
2. *nix

Installation
-------------
`go get github.com/verdverm/httopd/httopd`

Running
-----------

watching a single log file
`httopd -fn="/abs/path/to/log/file"`

watching a list of log files
`httopd -fnList="path/to/list/file"`

list file format
```
/abs/path/to/log/access.log
/abs/path/to/site/log/access.log
/abs/path/to/site/log/access.log
```


Simulator
------------

1. `git clone https://github.com/verdverm/httopd && cd httopd`
2. `sudo build.sh`
3. `sudo run.sh`


`sudo` is required for the docker commands (unless you run a non-sudo docker setup)

Enhancements / Issues / Todo's
------------------------------

Want to help out? Add or remove items from the following list.

- log file format
  -- multiple files / domains... how to handle?
  -- only handling access.log default from nginx
  -- what about error.log ?
  -- other log providers ?
- monitor multiple log files when there are multiple sites / server blocks
- there are race conditions on the statistics
  -- there is a single reader and a single writer
  -- shouldn't be too much of an issues since only one party reads and only one party writes
- page stats only update when new line_data shows up for that page
- add history and alerts to errors
- backfill with 10 minutes of history on startup
- sort by columns
- config file or directory inspection for log files / log directories
- ML triggers & alerts
- more configurable triggers / set from CLI / save to file?
- better log line parser
  -- simpler and more flexible
  -- only tested with nginx, need to check apache and others
- stats should be kept in something like an R data frame
  -- so that aggregates can be calculated more easily
  -- can rely on an external library for stats calculations
- there may be some errors now resulting from multiple log files
  -- multiple watchers are firing linedata to the stats over channels
  -- if they arrive in a 'bad' order (reverse alternations over a minute boundary)
  -- we will switch bins, but the next arrival (last minute) will end up in the current bin, not the last one
  -- should really determine the bin by the time stamp, and then index to it
  -- right now we are just adding to the current bin
  -- this will be an issue with backfilling, which once resolved, we can backfile file by file, and not worry about time

Subdir Details
------------

#### server

This docker contains a Python-Flask site.

#### client

This docker contains a http-client simulator.

#### httpod

This folder contains the httpod program code.

#### logs

a temporary directory created and destroyed by the simulator

References
---------------

1. [Logging Control In W3C httpd - Logfile Format](http://www.w3.org/Daemon/User/Config/Logging.html#common-logfile-format)
2. [termbox-go](https://github.com/nsf/termbox-go)
