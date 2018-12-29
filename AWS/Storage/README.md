# Storage

Object level storage(DB) vs block level storage(S3): 

- block level 
  - allows more fine tuned updates like to contact info 
  - DB restrictions and organiztion allows complex and faster queries
-  object level:
  -  will update the entire pic
  - no restrictions on data, can be huge files(up to 5TB)

## Amazon EBS(Elastic Block Storage)

Block Storage

is a general thing like SSD backed for databases form No-SQL to SQL or hard disk backed for throughput intensive

## EFS (Elastic File System)

Can attach massively parallel shared access file system to different EC2s, will be in the same subnet

Higher throughput and lower latency then S3