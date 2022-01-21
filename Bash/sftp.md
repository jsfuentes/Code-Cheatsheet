# Secure File Transfer Protocol

```bash
sftp -i "~/Desktop/pem/Slingshow-1.pem" ec2-user@ec2-54-229-73-137.us-west-1.compute.amazonaws.com
```

Opens a ssh shell on the remote host with limited functionality

Use regular bash cmds to move around(`ls`, `cd`)

`help` in sftp shows you the list of acceptable commands(limited bash)

### Put in EC2/remote server

```bash
put [local_filename]
put -r [local_directory]
```

#### Get from remote

```bash
get remoteFile localFile
```

## Local interaction

preface commands with l to run them locally i.e

`lpwd` => local directory

`lcd`, `lls` etc

node test_attendee join --host eta-staging.onrender.com -m -h -n 4 HkQm-QyN
