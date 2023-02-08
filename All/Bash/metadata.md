# Editing File Metadata

Metadata is like where a file was downloaded from and such:

## Editing

```
xattr -l file.flv
com.apple.metadata:kMDItemWhereFroms:
00000000  62 70 6C 69 73 74 30 30 A1 01 5F 11 01 7F 68 74  |bplist00.._...ht|
00000010  74 70 3A 2F 2F 73 31 73 64 6C 6F 64 30 35 33 2E  |tp://s1sdlod053.|
00000020  62 63 73 74 2E 63 64 6E 2E 73 31 73 2E 79 69 6D  |bcst.cdn.s1s.yim|
00000030  67 2E 63 6F 6D 2F 2F 73 31 73 6E 66 73 30 36 72  |g.com//s1snfs06r|
00000040  30 35 2F 30 30 35 2F 76 69 64 65 6F 73 65 61 72  |05/005/videosear|
00000050  63 68 2F 39 30 35 32 32 35 37 37 2E 66 6C 76 3F  |ch/90522577.flv?|
00000060  53 74 72 65 61 6D 49 44 3D 39 30 35 32 32 35 37  |StreamID=9052257|
...

xattr -w "com.apple.metadata:kMDItemWhereFroms"
  "http://topdocumentaryfilms.com/journey-edge-universe/" file.flv
```