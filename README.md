# log.lua
A tiny logging module for Lua. 

![screenshot from 2014-07-04 19 55 55](https://cloud.githubusercontent.com/assets/3920290/3484524/2ea2a9c6-03ad-11e4-9ed5-a9744c6fd75d.png)


## Installation
The [log.lua](log.lua?raw=1) file should be dropped into an existing project
and required by it.
```lua
log = require "log"
``` 


## Usage
log.lua provides 6 functions, each function takes all its arguments,
concatenates them into a string then outputs the string to the console and --
if one is set -- the log file.

|                     |                     |                     |
|---------------------|---------------------|---------------------|
| **log.trace(...)**  | **log.info(...)**   | **log.error(...)**  |
| **log.debug(...)**  | **log.warn(...)**   | **log.fatal(...)**  |
|                     |                     |                     |

It also provides a `log.check()`.  The function accepts the same
arguments as Lua's standard `assert()`, along with an optional third
argument naming the level at which to log the assertion.  For example:

```lua
log.check(x == y, "X and Y are not equal.", "debug")
```

This code is equivalent to:

```lua
if not x == y then
  log.debug("X and Y are not equal.")
end
```

If the third argument is nil then the function uses the value of
`warn`.  Like the standard `assert()` function, the `log.check()`
function will return the value of its first argument.

Similar the `assert()`, the second parameter is also optional, in
which case `log.check()` will default to the message `check failed`,
e.g. these examples are equivalent:

```lua
log.check(x == y)

log.check(x == y, "check failed", "warn)
```


### Additional options
log.lua provides variables for setting additional options:

#### log.usecolor
Whether colors should be used when outputting to the console, this is `true` by
default. If you're using a console which does not support ANSI color escape
codes then this should be disabled.

#### log.outfile
The name of the file where the log should be written, log files do not contain
ANSI colors and always use the full date rather than just the time. By default
`log.outfile` is `nil` (no log file is used). If a file which does not exist is
set as the `log.outfile` then it is created on the first message logged. If the
file already exists it is appended to.

#### log.level
The minimum level to log, any logging function called with a lower level than
the `log.level` is ignored and no text is outputted or written. By default this
value is set to `"trace"`, the lowest log level, such that no log messages are
ignored.

The level of each log mode, starting with the lowest log level is as follows:
`"trace"` `"debug"` `"info"` `"warn"` `"error"` `"fatal"`


## License
This library is free software; you can redistribute it and/or modify it under
the terms of the MIT license. See [LICENSE](LICENSE) for details.

