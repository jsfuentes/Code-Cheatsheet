# Helmet

Helmet helps you secure your Express apps by setting various HTTP headers

```bash
npm install helmet
```

By default does following:

| Module                                                       | Notes                                                        | Why                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| [frameguard](https://helmetjs.github.io/docs/frameguard/)    | tells browsers to prevent your webpage from being put in an iframe | to prevent clickjacking                                      |
| [hsts](https://helmetjs.github.io/docs/hsts/) for HTTP Strict Transport Security | won’t tell users on HTTP to *switch* to HTTPS, it will just tell HTTPS users to stick around | HTTP sucks                                                   |
| [ieNoOpen](https://helmetjs.github.io/docs/ienoopen) sets X-Download-Options for IE8+ | ✓                                                            |                                                              |
| [noSniff](https://helmetjs.github.io/docs/dont-sniff-mimetype) to keep clients from sniffing the MIME type | they will trust what the server says and block the resource if it’s wrong instead of guessing | if client recieves html(user uploaded data) even with wrong mime, it could run it |
| [xssFilter](https://helmetjs.github.io/docs/xss-filter) adds some small XSS protections | ✓                                                            |                                                              |
| [dnsPrefetchControl](https://helmetjs.github.io/docs/dns-prefetch-control) controls browser DNS prefetching | ✓                                                            |                                                              |

