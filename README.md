# tune10gb
Tune and benchmark network filesystem (NFS/CIFS/Web) performance of linux client network stack transfering large files to a 10Gb NAS (Network Attached Storage) server.
+
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
+

