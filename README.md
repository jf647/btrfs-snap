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

* mountpoint is the filesystem to snapshot
* prefix is the prefix, which usually corresponds to a schedule (e.g. 1m, 5m, 3h, 1d, 1w, 3mo)
* count is the number of snapshots with the same prefix to keep
* -r makes the snapshot readonly (requires btrfs-tools v0.20)
* -c generates more compatible snapshot names
     (ie. no colons that confuse SAMBA/Window$ clients)
* -d dir places the snapshot in dir, relative to the mountpoint
* -b basedir places the snapshot in basedir with a directory structure that mimics the mountpoint
* -B basedir places the snapshots in basedir with NO additional subdirectory structure

Without -b, -B, or -d, snapshots are placed in a directory called .snapshot at the top of the mountpoint.

mountpoint must be a mounted btrfs filesystem (i.e. appears in the output of
"mount -t btrfs") or an unmounted btrfs subvolume (which must exit 0 when
"btrfs su sh" is called on it).  Unmounted subvolumes require a recent
version of btrfs-progs; see "OS Support" below for specifics.

Examples
--------

```cron
*/5   *   *   *   *   btrfs-snap -r / 5m 12
0     0   *   *   *   btrfs-snap -r -b /snapshots /home 1d 7
```

The above cronjob would

1. create a snapshot of / every 5 minutes, keeping 12 generations in /.snapshot
1. create a snapshot of /home every day, keeping 7 generations in /snapshots/home

OS Support
----------

Tested on

* Ubuntu 12.04 with the raring kernel
* Ubuntu 13.04
* Debian 8

Anything else, YMMV.  Reports of successful use on other operating systems
is welcome

To snaphshot an unmounted btrfs subvolume, you need a version of btrfs-progs
that supports the "btrfs subvolume show" command.

The version that comes with Ubuntu 13.04 is too old; the version that comes
with Ubuntu 13.10 works.  You should be able to compile a working version
from the sources (refer to
https://btrfs.wiki.kernel.org/index.php/Btrfs_source_repositories for
details).

License
-------

This program is distributed under the GNU General Public License

http://www.gnu.org/licenses/gpl.txt

Authors
-------

Originally by Birger Monsen <birger@birger.sh>

Readonly and basedir additions by James FitzGibbon <james@nadt.net>

VFS snapshot naming support by gitmopp (https://github.com/gitmopp)

Support for snapshotting unmounted btrfs subvolumes by Brian Kloppenborg (https://github.com/bkloppenborg)
