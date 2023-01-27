# DESCRIPTION
bht is a script to help with bulk hdd testing using badblocks. when you need to fully test 24 or 48 or whatever number of hard drives at the same time with badblocks, bht makes this easy by launching multiple instances of badblocks in the background. you can periodically check on the status of all running instances of badblocks. you can even leave an email address so that when an instance of badblocks is done, you can receive an email notice with the results.

# REQUIREMENTS
i wrote bht on Linux with ksh93, so it requires the following to run:

- ksh93
- smartctl
- badblocks
- sha256sum
- lsscsi

along with a few standard Unix utilities like: mktemp, grep, awk, find, tail, mailx, ps, mkdir, mv, id.

On Debian, and derivative Linux distributions, this command should install all the requirements:
```
sudo apt-get install smartmontools lsscsi mailutils ksh lvm2
```
# HOW TO USE
first, create a directory to store your test data:
```
$ mkdir /path/to/test/data
```
change to that directory. make sure 'bht' is in your path, or call it with full path with a list of hard drives to test. note that you must run 'bht' as root or with root privileges (with sudo or su):
```
$ cd /path/to/test/data
$ bht /dev/sda /dev/sdb /dev/sdc /dev/sdd
```
you will be prompted to confirm the test run, as it will destroy any data on the hard drives. once you confirm, badblocks will be launched in the background for each hard drive.

to check on the status of the test run, execute 'bht' with --status option:
```
$ cd /path/to/test/data
$ bht --status
```
you can stop the tests with the --terminate option:
```
$ cd /path/to/test/data
$ bht --terminate
```
# EXAMPLE
to run the test:
```
$ mkdir /var/tmp/bht-data
$ cd /var/tmp/bht-data
$ bht /dev/sda /dev/sdb /dev/sdc /dev/sdd /dev/sde /dev/sdf /dev/sdg /dev/sdh
INFO: changing to /var/tmp/bht-data.
ATTN: this hard drive testing process will wipe all data
ATTN: on the following hard drives:
ATTN: /dev/sda /dev/sdb /dev/sdc /dev/sdd /dev/sde /dev/sdf /dev/sdg /dev/sdh
ATTN: ARE YOU SURE YOU WANT TO PROCEED?: y
INFO: collecting SMART data from each drive.
INFO: MAXTORSTM3500630AS / 9QG03B71
INFO: MAXTORSTM3500630AS / 9QG07KSW
INFO: MAXTORSTM3500630AS / 9QG06Y9T
INFO: MAXTORSTM3500630AS / 9QG07NY1
INFO: MAXTORSTM3500630AS / 9QG0481X
INFO: MAXTORSTM3500630AS / 9QG07MBJ
INFO: WDCWD5002ABYS-01B1B0 / WD-WCASY4156094
INFO: MAXTORSTM3500630AS / 9QG04LGB
INFO: Running badblocks on /dev/sda.
INFO: ==> output to /var/tmp/bht-data/disks/MAXTORSTM3500630AS_9QG03B71.
INFO: ==> [MAXTORSTM3500630AS|9QG03B71]
INFO: Running badblocks on /dev/sdb.
INFO: ==> output to /var/tmp/bht-data/disks/MAXTORSTM3500630AS_9QG07KSW.
INFO: ==> [MAXTORSTM3500630AS|9QG07KSW]
INFO: Running badblocks on /dev/sdc.
INFO: ==> output to /var/tmp/bht-data/disks/MAXTORSTM3500630AS_9QG06Y9T.
INFO: ==> [MAXTORSTM3500630AS|9QG06Y9T]
INFO: Running badblocks on /dev/sdd.
INFO: ==> output to /var/tmp/bht-data/disks/MAXTORSTM3500630AS_9QG07NY1.
INFO: ==> [MAXTORSTM3500630AS|9QG07NY1]
INFO: Running badblocks on /dev/sde.
INFO: ==> output to /var/tmp/bht-data/disks/MAXTORSTM3500630AS_9QG0481X.
INFO: ==> [MAXTORSTM3500630AS|9QG0481X]
INFO: Running badblocks on /dev/sdf.
INFO: ==> output to /var/tmp/bht-data/disks/MAXTORSTM3500630AS_9QG07MBJ.
INFO: ==> [MAXTORSTM3500630AS|9QG07MBJ]
INFO: Running badblocks on /dev/sdg.
INFO: ==> output to /var/tmp/bht-data/disks/WDCWD5002ABYS-01B1B0_WD-WCASY4156094.
INFO: ==> [WDCWD5002ABYS-01B1B0|WD-WCASY4156094]
INFO: Running badblocks on /dev/sdh.
INFO: ==> output to /var/tmp/bht-data/disks/MAXTORSTM3500630AS_9QG04LGB.
INFO: ==> [MAXTORSTM3500630AS|9QG04LGB]
```
to check on status:
```
$ bht --status
MAXTORSTM3500630AS_9QG03B71:
	badblocks[Testing with pattern 0xaa   0.64% done, 0:42 elapsed. (0/0/0 errors)]
	SMART:[Reallocated_Sector_Ct=0]
	SMART:[Power_On_Hours=14208]
	SMART:[Multi_Zone_Error_Rate=0]
MAXTORSTM3500630AS_9QG07KSW:
	badblocks[Testing with pattern 0xaa   0.64% done, 0:42 elapsed. (0/0/0 errors)]
	SMART:[Reallocated_Sector_Ct=0]
	SMART:[Power_On_Hours=14208]
	SMART:[Multi_Zone_Error_Rate=0]
MAXTORSTM3500630AS_9QG06Y9T:
	badblocks[Testing with pattern 0xaa   0.64% done, 0:42 elapsed. (0/0/0 errors)]
	SMART:[Reallocated_Sector_Ct=0]
	SMART:[Power_On_Hours=14208]
	SMART:[Multi_Zone_Error_Rate=0]
MAXTORSTM3500630AS_9QG07NY1:
	badblocks[Testing with pattern 0xaa   0.66% done, 0:42 elapsed. (0/0/0 errors)]
	SMART:[Reallocated_Sector_Ct=0]
	SMART:[Power_On_Hours=14209]
	SMART:[Multi_Zone_Error_Rate=0]
MAXTORSTM3500630AS_9QG0481X:
	badblocks[Testing with pattern 0xaa   0.66% done, 0:42 elapsed. (0/0/0 errors)]
	SMART:[Reallocated_Sector_Ct=0]
	SMART:[Power_On_Hours=14209]
	SMART:[Multi_Zone_Error_Rate=0]
MAXTORSTM3500630AS_9QG07MBJ:
	badblocks[Testing with pattern 0xaa   0.68% done, 0:42 elapsed. (0/0/0 errors)]
	SMART:[Reallocated_Sector_Ct=0]
	SMART:[Power_On_Hours=14209]
	SMART:[Multi_Zone_Error_Rate=0]
WDCWD5002ABYS-01B1B0_WD-WCASY4156094:
	badblocks[Testing with pattern 0xaa   0.99% done, 0:42 elapsed. (0/0/0 errors)]
	SMART:[Reallocated_Sector_Ct=2]
	SMART:[Power_On_Hours=54979]
	SMART:[Multi_Zone_Error_Rate=0]
MAXTORSTM3500630AS_9QG04LGB:
	badblocks[Testing with pattern 0xaa   0.67% done, 0:42 elapsed. (0/0/0 errors)]
	SMART:[Reallocated_Sector_Ct=0]
	SMART:[Power_On_Hours=14208]
	SMART:[Multi_Zone_Error_Rate=0]
```
to stop the tests:
```
$ bht --terminate
MAXTORSTM3500630AS_9QG03B71: terminating PID=7388.
MAXTORSTM3500630AS_9QG07KSW: terminating PID=7390.
MAXTORSTM3500630AS_9QG06Y9T: terminating PID=7392.
MAXTORSTM3500630AS_9QG07NY1: terminating PID=7394.
MAXTORSTM3500630AS_9QG0481X: terminating PID=7396.
MAXTORSTM3500630AS_9QG07MBJ: terminating PID=7398.
WDCWD5002ABYS-01B1B0_WD-WCASY4156094: terminating PID=7399.
MAXTORSTM3500630AS_9QG04LGB: terminating PID=7400.
```
# OTHER OPTIONS
if you provide an email address with --email option, when an instance of badblocks is done, you will receive an email notice with the results. please note that this relies on the mailx command to work, so your local mail relaying capability must be working. here's an example
```
$ bht --email me@domain.com /dev/sda /dev/sdb /dev/sdc /dev/sdd /dev/sde /dev/sdf /dev/sdg /dev/sdh
```
when badblocks is complete, you will receive an email that looks like this:
```
Model=MAXTORSTM3500630AS, Serial=9QG04LGB
badblocks[Testing with pattern 0xaa Interrupted at block 74752]
SMART:[Reallocated_Sector_Ct=0]
SMART:[Power_On_Hours=14208]
SMART:[Multi_Zone_Error_Rate=0]
```
by default, bht uses your current working directory as the test data directory. so, as in the examples above, you should change to the test data directory before running 'bht'. this way, you can have multiple test data directories and bht will handle them separately. there is also a way to specify the data directory without having to change directories each time with the --directory option:
```
$ bht --directory /var/tmp/bht-data2 --status
```
the above command will show the status of the test data in /var/tmp/bht-data2.

to see all options available, use the --help option:
```
$ bht --help
Usage: bht [ options ]
OPTIONS
  -b, --blocks=blocks
                  the size of blocks in bytes. The default value is 32768.
  -n, --stride=stride
                  the number of blocks per test. The default value is 512.
  -e, --email=email
                  email address to send notifications.
  -s, --status    show status of current tests.
  -d, --directory=directory
                  path to directory with bht data. defaults to current working directory.
  -t, --terminate terminate all running tests.
```
