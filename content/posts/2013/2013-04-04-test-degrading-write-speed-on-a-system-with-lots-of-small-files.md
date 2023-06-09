---
title: Test degrading write speed on a system with lots of small files.
author: silviu
type: post
date: 2013-04-04T10:43:23+00:00
url: /2013/04/04/test-degrading-write-speed-on-a-system-with-lots-of-small-files/
categories:
  - old
tags:
  - temp_on

---
I created a script that generates random files in a random folder structure. I let it run for 1.000.000 files and than 1.000.000 more. Here are the results:

```bash
#!/bin/bash
DST=$(mktemp -tmpdir="/tmp/boatload" -d XXXXXXXXXX)

let "no_of_files = $RANDOM/2"
echo "Creating $no_of_files files in $DST"

counter=1
while [[ $counter -le $no_of_files ]]; do
# echo Creating file no $counter
# dd bs=64 count=$RANDOM skip=$RANDOM if=/dev/xvda2 of=$DST/random-file.$counter; # this is useful for big files
  let "CNT = $RANDOM/40"
  dd bs=8 count=$CNT if=/dev/urandom of=$DST/random-file.$counter > /dev/null 2>&1
  let "counter += 1";
done

echo "Created $counter files in $DST" >> /app/scripts/file_generator.log

cat /app/scripts/file_generator.log | awk '{ print $2 }' | paste -sd+ | bc
```

And the test script:

```bash
#!/bin/bash

if [ $# -eq 1 ]; then
# assume the parameter is the log file
  LOG="$1"
else
  LOG="./stats.out"
fi

>"$LOG"

echo "Performing dd tests..."

COUNT=$(( $(awk '/MemTotal/ { print $2 }' /proc/meminfo) * 2 / 1024 ))
for i in {1..5}; do dd if=/dev/zero of=/tmp/dd bs=12M count=$(($COUNT/12)) oflag=direct 2>&1 | grep bytes; done >> "$LOG"
for i in {1..5}; do dd if=/tmp/dd of=/dev/null 2>&1 | grep bytes; done >> "$LOG"
```

And the results on a 1Gb RAM virtual machine:

```bash
#start:
2076180480 bytes (2.1 GB) copied, 3.32403 s, 625 MB/s
2076180480 bytes (2.1 GB) copied, 3.67567 s, 565 MB/s
2076180480 bytes (2.1 GB) copied, 3.27064 s, 635 MB/s
2076180480 bytes (2.1 GB) copied, 3.08417 s, 673 MB/s
2076180480 bytes (2.1 GB) copied, 3.47598 s, 597 MB/s
2076180480 bytes (2.1 GB) copied, 14.2744 s, 145 MB/s
2076180480 bytes (2.1 GB) copied, 14.0241 s, 148 MB/s
2076180480 bytes (2.1 GB) copied, 13.9492 s, 149 MB/s
2076180480 bytes (2.1 GB) copied, 13.8386 s, 150 MB/s
2076180480 bytes (2.1 GB) copied, 14.6904 s, 141 MB/s

#After 1.000.000 extra files
2076180480 bytes (2.1 GB) copied, 4.57828 s, 453 MB/s
2076180480 bytes (2.1 GB) copied, 4.94669 s, 420 MB/s
2076180480 bytes (2.1 GB) copied, 4.507 s, 461 MB/s
2076180480 bytes (2.1 GB) copied, 4.83228 s, 430 MB/s
2076180480 bytes (2.1 GB) copied, 4.50465 s, 461 MB/s
2076180480 bytes (2.1 GB) copied, 14.3866 s, 144 MB/s
2076180480 bytes (2.1 GB) copied, 14.0353 s, 148 MB/s
2076180480 bytes (2.1 GB) copied, 14.0053 s, 148 MB/s
2076180480 bytes (2.1 GB) copied, 13.7696 s, 151 MB/s
2076180480 bytes (2.1 GB) copied, 15.8247 s, 131 MB/s

#After 2.000.000 extra files
2076180480 bytes (2.1 GB) copied, 6.06685 s, 342 MB/s
2076180480 bytes (2.1 GB) copied, 6.24056 s, 333 MB/s
2076180480 bytes (2.1 GB) copied, 5.36537 s, 387 MB/s
2076180480 bytes (2.1 GB) copied, 5.21678 s, 398 MB/s
2076180480 bytes (2.1 GB) copied, 5.25093 s, 395 MB/s
2076180480 bytes (2.1 GB) copied, 17.429 s, 119 MB/s
2076180480 bytes (2.1 GB) copied, 16.3595 s, 127 MB/s
2076180480 bytes (2.1 GB) copied, 15.4667 s, 134 MB/s
2076180480 bytes (2.1 GB) copied, 15.8035 s, 131 MB/s
2076180480 bytes (2.1 GB) copied, 15.0656 s, 138 MB/s
```