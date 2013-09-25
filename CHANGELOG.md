# btrfs-snap Changelog

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
