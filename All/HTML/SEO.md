# SEO

In the head tag, good to include a descriptive title and meta description

```html
<meta name="description" content="The publishing platform for developers offering compelling coding articles and articles. This isn't just another blogging platform offering deep integrations with coding languages and tools. " />
<title>Modulo - The Publishing Platform for Developers</title>
```

[Special Tags that google understands](https://support.google.com/webmasters/answer/79812)

### Dynamically Setting Meta

Most crawlers just use the server direct meta tag. Can't use something like react helmet here. Should set on server so when pinged directly works. Its fine that react-router redirection doesn't update meta, you care about crawlers accessing directly. 

https://create-react-app.dev/docs/title-and-meta-tags/#generating-dynamic-meta-tags-on-the-server