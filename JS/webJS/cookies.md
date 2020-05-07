# Cookies?

```js
document.cookie= "username=John Doe; expires=Thu, 18 Dec 2013 12:00:00 UTC"; 
```

### [Read all cookies accessible from this location](https://developer.mozilla.org/en-US/docs/Web/API/Document/cookie#Read_all_cookies_accessible_from_this_location)

```
allCookies = document.cookie;
```

In the code above `*allCookies*`is a string containing a semicolon-separated list of all cookies (i.e. `key=value`pairs). Note that each keyand value may be surrounded by whitespace (space and tab characters): in fact, [RFC 6265](https://tools.ietf.org/html/rfc6265)mandates a single space after each semicolon, but some user agents may not abide by this.

### [Write a new cookie](https://developer.mozilla.org/en-US/docs/Web/API/Document/cookie#Write_a_new_cookie)

```
document.cookie = newCookie;
```

In the code above, `newCookie`is a string of form `key=value`