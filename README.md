# btrfs-subvolume-usage
Shell script to display btrfs subvolume usage information in a more usable way than the btrfs tool.

## Contributions
Contributions are welcomed.

## Usage

```
$ btrfs-subvolume-usage --help
Usage: /usr/local/bin/btrfs-subvolume-usage [OPTIONS]
 OPTIONS
 -h  --help --usage      : Show this usage information.
 --version               : Show the version information.
 -pPATH --path=PATH      : Path to a mounted btrfs file system (default: /).
 -h0|1 --header=on|off   : Turn on/off the header (default: on).
 -p0|1 --padding=on|off  : Turn on/off the column padding (default: on).
 -rs  --reverse-sort     : Reverse sort order.
 -sN   --sort=N          : Sort the rows using the Nth column (default: last column).
 -sCID --sort=CID        : Sort the rows using the CID column.
 -cCID:* --columns=CID:* : Colon separated list of column IDs to display
                           (default: display all).
 Column IDs (CID)        : QGROUPID, TOTAL, EXCLUSIVE, SHARED, SHARED%, PATH.
```

## Examples

```
$ btrfs-subvolume-usage -sSHARED%
qgroup ID total  MB exclusive MB shared MB shared % path
========= ========= ============ ========= ======== ====
0/260           390          390         0        0 root/var/tmp
0/259            71           70         0        1 root/var/log
0/2406         7564           11      7552       99 .snapshots/root/2017-08-31___backup
0/2407        37080          141     36939       99 .snapshots/root/user/test/2017-08-31___backup
0/2412         7564            7      7557       99 .snapshots/root/2017-09-01___backup
0/2413        37093           50     37043       99 .snapshots/root/user/test/2017-09-01___backup
0/257          7569           11      7557       99 root
0/313         37095           66     37028       99 root/home/test
```

```
$ btrfs-subvolume-usage -sPATH -cTOTAL:EXCLUSIVE:PATH
total  MB exclusive MB path
========= ============ ====
        0            0 
     7569           11 root
    37096           68 root/home/user
       71           70 root/var/log
      390          390 root/var/tmp
     7564           11 .snapshots/root/2017-08-31___backup
     7564            7 .snapshots/root/2017-09-01___backup
    37080          141 .snapshots/root/home/user/2017-08-31___backup
    37093           50 .snapshots/root/home/user/2017-09-01___backup
```
