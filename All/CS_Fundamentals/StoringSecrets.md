# Storing Secrets

There are many heavy weight solutions that you should look into if you become a team with many credentials including blackbox, https://www.chef.io/, https://square.github.io/keywhiz/. Can also have files encrypted on github with things like git-crypt 

## Simple Solutions

### Environment Variables

- easy load from file
- often use env variables for other things too so good to set up

Cons:

- According to https://news.ycombinator.com/item?id=9952911, its possible that environment variables are shown in debug output when a server crashes potentially comprising the system
- Can't revoke secrets.json or manage like an expert

### Seperate Secrets.json

- Easiest 

