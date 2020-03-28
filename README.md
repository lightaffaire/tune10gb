# tune10gb
Tune and benchmark network filesystem (NFS/CIFS/Web) performance of linux client network stack transfering large files to and from a 10Gb NAS (Network Attached Storage) server.
```
Usage: tune10gb [options]
       test:
       -a       run all performance tests (all=dsk+web+nfs+cifs)
       -t type  run performance test type(s) from perf typelist
       -n num   run performance test(s) N times (default: 1)
       -s size  data file size in [KMG]B (default: 10GB)
       -b size  block size in [KMG]B (default: 64KB)

       setup:
       -G       get OS + config settings
       -S       set OS + config settings
       -R       reset OS + config settings

       misc:
       -l       list config file (file:///root/.tune10gb)
       -e       edit config file
       -c       cleanup test files

       -v       verbose

Performance test type list (-t option):
[all|
dsk|web|nfs|cifs|
dskcat|dskget|dskput|dskmix|
webcat|webget|
nfstcp|nfstcpcat|nfstcpget|nfstcpput|nfstcpmix|
nfsudp|nfsudpcat|nfsudpget|nfsudpput|nfsudpmix|
cifscat|cifsget|cifsput|cifsmix]

Examples:

$ tune10gb -a -s 20G

$ tune10gb -t nfstcp -t cifs -n 5
``` 
```
$ tune10gb -t "nfstcp cifs" -s 25gb -n 3

RUN: fallocate -l 25GB /tune10gb_25GB.data

NFS TCP: 192.168.10.4:/volume1/data  /nfs-tcp  nfs  rsize=65536  wsize=65536  tcp

RUN[3/3]: nfs tcp cat 25GB  [/nfs-tcp/test/tune10gb_25GB.data] > [/dev/null] [bs=64KB]
RAN[1/3]: nfs tcp cat 25GB  I/O:  62.15s @   384 MB/s
RAN[2/3]: nfs tcp cat 25GB  I/O:  50.41s @   473 MB/s
RAN[3/3]: nfs tcp cat 25GB  I/O:  50.65s @   471 MB/s
AVG[3/3]: nfs tcp cat 25GB  I/O:  54.40s @   443 MB/s

RUN[3/3]: nfs tcp get 25GB  [/nfs-tcp/test/tune10gb_25GB.data] > [/tune10gb_25GB.data] [bs=64KB]
RAN[1/3]: nfs tcp get 25GB  I/O:  67.50s @   353 MB/s
RAN[2/3]: nfs tcp get 25GB  I/O:  65.47s @   364 MB/s
RAN[3/3]: nfs tcp get 25GB  I/O:  55.46s @   430 MB/s
AVG[3/3]: nfs tcp get 25GB  I/O:  62.81s @   382 MB/s

RUN[3/3]: nfs tcp put 25GB  [/tune10gb_25GB.data] > [/nfs-tcp/test/tune10gb_25GB.data] [bs=64KB]
RAN[1/3]: nfs tcp put 25GB  I/O:  27.63s @   863 MB/s
RAN[2/3]: nfs tcp put 25GB  I/O:  28.82s @   827 MB/s
RAN[3/3]: nfs tcp put 25GB  I/O:  28.13s @   848 MB/s
AVG[3/3]: nfs tcp put 25GB  I/O:  28.19s @   846 MB/s

RUN[3/3]: nfs tcp r+w 25GB  [/nfs-tcp/test/tune10gb_25GB.data] > [/nfs-tcp/test/tune10gb_temp_25GB.data] [bs=64KB]
RAN[1/3]: nfs tcp r+w 25GB  I/O: 109.91s @   217 MB/s
RAN[2/3]: nfs tcp r+w 25GB  I/O:  95.16s @   251 MB/s
RAN[3/3]: nfs tcp r+w 25GB  I/O:  94.75s @   252 MB/s
AVG[3/3]: nfs tcp r+w 25GB  I/O:  99.94s @   240 MB/s

CIFS: //192.168.10.4/data  /cifs  cifs  rw,vers=3

RUN[3/3]: cifs cat 25GB  [/cifs/test/tune10gb_25GB.data] > [/dev/null] [bs=64KB]
RAN[1/3]: cifs cat 25GB  I/O:  30.90s @   772 MB/s
RAN[2/3]: cifs cat 25GB  I/O:  33.10s @   720 MB/s
RAN[3/3]: cifs cat 25GB  I/O:  29.40s @   811 MB/s
AVG[3/3]: cifs cat 25GB  I/O:  31.13s @   768 MB/s

RUN[3/3]: cifs get 25GB  [/cifs/test/tune10gb_25GB.data] > [/tune10gb_25GB.data] [bs=64KB]
RAN[1/3]: cifs get 25GB  I/O:  35.28s @   676 MB/s
RAN[2/3]: cifs get 25GB  I/O:  38.18s @   624 MB/s
RAN[3/3]: cifs get 25GB  I/O:  37.95s @   628 MB/s
AVG[3/3]: cifs get 25GB  I/O:  37.13s @   643 MB/s

RUN[3/3]: cifs put 25GB  [/tune10gb_25GB.data] > [/cifs/test/tune10gb_25GB.data] [bs=64KB]
RAN[1/3]: cifs put 25GB  I/O:  25.31s @   942 MB/s
RAN[2/3]: cifs put 25GB  I/O:  29.39s @   811 MB/s
RAN[3/3]: cifs put 25GB  I/O:  26.14s @   912 MB/s
AVG[3/3]: cifs put 25GB  I/O:  26.94s @   888 MB/s

RUN[3/3]: cifs r+w 25GB  [/cifs/test/tune10gb_25GB.data] > [/cifs/test/tune10gb_temp_25GB.data] [bs=64KB]
RAN[1/3]: cifs r+w 25GB  I/O:  46.38s @   514 MB/s
RAN[2/3]: cifs r+w 25GB  I/O:  72.99s @   327 MB/s
RAN[3/3]: cifs r+w 25GB  I/O:  72.76s @   328 MB/s
AVG[3/3]: cifs r+w 25GB  I/O:  64.04s @   390 MB/s
```
