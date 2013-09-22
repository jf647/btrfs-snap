btrfs-snap
==========

btrfs-snap creates and maintains the history of snapshots of btrfs filesystems.

Features:

* can snapshot inside of the filesystem or rooted in a base directory
* can purge old snapshots when too many exist
* can keep multiple snapshot schedules for the same filesystem

btrfs-snap is designed to be called from cron on a regular schedule.

Usage
-----

btrfs-snap [-r] [-b basedir] mountpoint prefix count

* mountpoint is the filesystem to snapshot (must be found in the output of 'mount -t btrfs')
* prefix is the prefix, which usually corresponds to a schedule (e.g. 1m, 5m, 3h, 1d, 1w, 3mo)
* count is the number of snapshots with the same prefix to keep
* -r makes the snapshot readonly (requires btrfs-tools v0.20)
* -b basedir places the snapshot in a like-named directory rooted in the basedir.  Without -b, snapshots are placed in a directory called .snapshot at the top of the mountpoint

Examples
--------

```cron
*/5   *   *   *   *   btrfs-snap -r / 5m 12
0     0   *   *   *   btrfs-snap -r -b /snapshots /home 1d 7
```

The above cronjob would

1. create a snapshot of / every 5 minutes, keeping 12 generations in /.snapshot
1. create a snapshot of / every day, keeping 7 generations in /snapshots/home

OS Support
----------

Tested on

* Ubuntu 12.04 with the raring kernel
* Ubuntu 13.04

Anything else, YMMV.  Reports of successful use on other operating systems is welcome

License
-------

This program is distributed under the GNU General Public License

http://www.gnu.org/licenses/gpl.txt

Authors
-------

Originally by Birger Monsen <birger@birger.sh>

Readonly and basedir additions by James FitzGibbon <james@nadt.net>

VFS snapshot naming support by gitmopp (https://github.com/gitmopp)
