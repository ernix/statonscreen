statonscreen
============

screen hardstatusline indicator for testing

DESCRIPTION
-----------

`statonscreen` assumes that you use `gnu screen` and turn on hardstatus line, 
the default format line is ``%`%-w%{=b kw}%n %t%{-}%+w``.

USAGE
-----

Create some scripts to monitor file changes and test your project, like:

```perl
use warnings;
use strict;

use Filesys::Notify::Simple;
use Cwd 'realpath';

my $watcher = Filesys::Notify::Simple->new([ "." ]);

$SIG{INT} = $SIG{HUP} = $SIG{QUIT} = $SIG{TERM} = $SIG{PIPE} = sub {
    system("path/to/statonscreen -c");
    exit;
};

while(1) {
    my $c = 0;
    $watcher->wait(sub { ++$c for @_ });
    if ($c) {
        system("path/to/statonscreen -e 'prove'");
    }
}
```
