# Zipping

## ZIP

- most commonly used archiving format out there today

- available on all OSs
- not best compression

Compress:

`zip -r archive_name.zip directory_to_compress`

Extract:

`unzip archive_name.zip`

## TAR

- common on Linux
- consumes very little time and CPU to compress files,
- compression minor

Compress:

`tar -cvf archive_name.tar directory_to_compress`

Extract:

`tar -xvf archive_name.tar.gz`

Extract to specific dir

`tar -xvf archive_name.tar -C /tmp/extract_here/`

## TAR.GZ

- pretty great with good compression and not too much CPU

Compress:

`tar -zcvf archive_name.tar.gz directory_to_compress`

Extract:

\# **tar -zxvf archive_name.tar.gz**

Extract to specific dir:

\# **tar -zxvf archive_name.tar.gz -C /tmp/extract_here/**

## TAR.BZ2

- best compression with most CPU

`tar -jcvf archive_name.tar.bz2 directory_to_compress`

Extract to specific dir:

`tar -jxvf archive_name.tar.bz2 -C /tmp/extract_here/`