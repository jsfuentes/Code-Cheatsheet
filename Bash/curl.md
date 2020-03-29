# Curl

Transfer data with all these protocols: DICT, FILE, FTP, FTPS, GOPHER, HTTP, HTTPS, IMAP, IMAPS, LDAP, LDAPS, POP3, POP3S, RTMP, RTSP, SCP, SFTP, SMB, SMBS, SMTP, SMTPS, TELNET and TFTP

```bash
curl https://api.mux.com/video/v1/assets \
  -H "Content-Type: application/json" \
  -X POST \
  -d '{ "input": "{URL_TO_VIDEO_ASSET}", "playback_policy": "public" }' \
  -u {MUX_TOKEN_ID}:{MUX_TOKEN_SECRET} | json_pp
```

`json_pp` takes json and outputs pretty printed json