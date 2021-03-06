# win32-taskscheduler gem

[![Gem Version](https://badge.fury.io/rb/win32-taskscheduler.svg)](https://badge.fury.io/rb/win32-taskscheduler)
[![Build status](https://ci.appveyor.com/api/projects/status/3bh741beu9bl9g87/branch/ole?svg=true)](https://ci.appveyor.com/project/chef/win32-taskscheduler/branch/ole)

The win32-taskscheduler library is a Ruby interface to the MS Windows Task Scheduler. It is analogous to the Unix cron daemon.

# Installation

```
gem install win32-taskscheduler
```

# Synopsis

```ruby
require 'win32/taskscheduler'
include Win32

ts = TaskScheduler.new

# Create a trigger that starts on April 25, 2014 at 11:05 pm. The trigger
# will run on the first and last week of the month, on Monday and Friday,
# in the months of April and May.
#
trigger = {
  :start_year   => 2014,
  :start_month  => 4,
  :start_day    => 25,
  :start_hour   => 23,
  :start_minute => 5,
  :trigger_type => TaskScheduler::MONTHLYDOW,
  :type => {
    :weeks        => TaskScheduler::FIRST_WEEK | TaskScheduler::LAST_WEEK,
    :days_of_week => TaskScheduler::MONDAY | TaskScheduler::FRIDAY,
    :months       => TaskScheduler::APRIL | TaskScheduler::MAY
  }
}

ts.new_work_item('my_notepad', trigger)
ts.application_name = 'notepad.exe'
ts.activate('my_notepad')
```

# Documentation

If you installed this library as a gem then the documentation was built for you and can be viewed if your gem server is running. There is also some documentation on the github wiki page.

# Acknowledgements

This library was modeled to some degree on the Win32::TaskScheduler Perl module by Umberto Nicoletti. However, there are some differences. Please see the documentation for details.

# Warranty

This package is provided "as is" and without any express or implied warranties, including, without limitation, the implied warranties of merchantability and fitness for a particular purpose.

# Known Issues

Some versions of Ruby have been known to segfault when attempting to create a task. If this happens you will need to upgrade your version of Ruby. Or, at least, your version of win32ole.

In some cases JRuby appears to raise a native exception rather than a Ruby exception on failure. This should be mostly harmless.

Please submit any bug reports to the project page at:

<http://github.com/chef/win32-taskscheduler>

# Copyright

- (C) 2003-2017 Daniel J. Berger All Rights Reserved
- (C) 2018 Chef Software, Inc. All Rights Reserved

# License

Artistic 2.0

# Authors

- Park Heesob
- Daniel Berger
