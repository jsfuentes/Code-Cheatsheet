# Zeit Now

```bash
npm i -g now
```

Zeit ez, first deploy is prod else dev

```bash
now #will link autolink to zeit/github project
now -e KEY=value #include env variables
now --prod #prod deployment
```

Use to include environment variables

Look in main folders now.json for variables like the project name

## Domains

1. In the GUI online, you can import from a github repo easily
2. You can then click settings, domains to add a domain

OR

```
now domains add <domain>
```

3. Get www redirect: Add www.jsfuentes.com AND jsfuentes.com, then go to GUI domains and set a redirect from www to jsfuentes



