# Setup

## Local Setup

Can install with brew `brew install postgresql`, follow instructions onscreen(`brew services start postgresql` & `initdb /usr/local/var/postgres` )

`postgres -V`

`psql` to enter cml

## On Server

[GCP guide](https://cloud.google.com/community/tutorials/setting-up-postgres) 

1) Create Ubuntu server on whatever Cloud Provider with some hard disk space or something idk

2) Install postgres

```bash
sudo apt update
sudo apt -y install postgresql postgresql-client postgresql-contrib
```

3) Setup user

Default user is `postgres`, but you need to set the password as it doesn't have one

```bash
sudo -u postgres psql postgres
\password postgres
#add password
CREATE EXTENSION adminpack; #enables server instrumentation
\q
```

4) Edit `pg_hba.conf` 

```bash
sudo nano /etc/postgresql/12/main/pg_hba.conf
```

 [ip4.me](http://ip4.me/) => Get your ipv4 address

```
# IPv4 remote connections for the tutorial:
host    all             all           [YOUR_IPV4_ADDRESS]/32         md5
```

5) Edit `postgresql.conf` to listen on all IP addresses

```bash
sudo nano /etc/postgresql/12/main/postgresql.conf
```

Find the line: 

```bash
#listen_addresses = 'localhost'
```

And turn into:

```bash
listen_addresses = '*'
```

Save, exit, and restart in bash

```bash
sudo service postgresql restart
```

6) For your cloud provider make sure the server can be accessed by all IPs