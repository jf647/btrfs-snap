# btrfs-snap Changelog
## v1.7.3 (Jul 25 2017)
* Removed perl dependency (replaced perl regex by bash regex)

## v1.7.2 (Feb 11 2017)
* Added new switch -q which makes output cron-compatible: silent unless an error occurs.
* Regex fix: correctly remove trailing slashes on mount-points

## v1.7.1 (Mar 16 2016)
* Fixed timestamp-bug (introduced in v1.6.1)

## v1.7.0 (Mar 14 2016)
* Added new switch -E which treats omitting a snapshot as an error.

## v1.6.1 (Mar 14 2016)
* Bugfix: touch to update the timestamp is only needed for option '-t'.
  For '-T' it is counter-productive and therefore disabled.

## v1.6.0 (Mar 09 2016)
* Added new flag -T which uses the transaction ids of btrfs to decide if new data is present.

## v1.5.0 (Mar 09 2016)
* Added new flag -p to use the <prefix> as a postfix.

## v1.4.2 (Feb 19 2016)
* Bugfix for prefix VFS: Removed an unneccessary $-sign which broke the code. (Thanks to 'clawes' for reporting.)

## v1.4.1 (Aug 31 2015)
* Bugfix for switch -t: Force update of source timestamp to prevent outdated timestamps on the folders

## v1.4.0 (Aug 28 2015)
* Added checks for existing snapshots and use pattern to search for existing snapshots
* Added a switch -B to specify the full path snapshot path
* Added a switch -t time to create only a snapshot if the newest already existing snapshot is older than 'time' seconds.
* Added PATH since script is most likely called by crontab with reduced PATH-settings

## v1.3.2 (Jan 10 2015)
* added switch to generate more compatible snapshot names
  (no colons in file names: this confuses SAMBA/Windows clients)

## v1.3.1 (Jan 05 2015)

* added switch to override default snapshot directory name ".snapshot"
* cleanup

## v1.2.2 (Sept 24 2013)

* trailing slash removal failed on multipart paths due to missing line
  terminator.  Time for a bats test suite.

## v1.2.1 (Sept 24 2013)

* fix trailing slash removal so that it works when the mountpoint is '/'.
  This required a change to perl from sed (standard sed doesn't have negated
  character classes)

## v1.2.0 (Sept 21 2013)

* added VFS snapshot naming support courtesy of gitmopp

## v1.1.0 (July 30 2013)

* add README
* add readonly snapshot and base directory features

## v1.0.0 (July 20 2013)

* Initial version written by Birger Monsen <birger@birger.sh>
