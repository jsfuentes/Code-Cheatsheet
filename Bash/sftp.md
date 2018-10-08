# Secure File Transfer Protocol

```bash
sftp sammy@your_server_ip_or_remote_hostname
```

Opens a ssh shell on the remote host with limited functionality

Use regular bash cmds to move around(`ls`, `cd`)

`help` in sftp shows you the list of acceptable commands(limited bash)

## Get 

```
get remoteFile localFile
```



## Local interaction

preface commands with l to run them locally i.e

`lpwd` => local directory

`lcd`, `lls` etc

