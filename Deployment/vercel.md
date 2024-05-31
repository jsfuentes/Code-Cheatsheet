# Vercel

```bash
npm i -g vercel
```

Zeit ez, first deploy is prod else dev

```bash
vercel #will link autolink to zeit/github project
vercel -e KEY=value #include env variables
vercel --prod #prod deployment
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

## [Analytics](https://vercel.com/docs/concepts/analytics/quickstart)

Comes with analytics

