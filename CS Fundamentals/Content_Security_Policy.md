# Content Security Policy

## Examples

```csp
Content-Security-Policy: script-src 'self' https://apis.google.com
```

### Overview

- **base-uri** restricts the URLs that can appear in a page’s `<base>` element.
- **child-src** lists the URLs for workers and embedded frame contents. For example: `child-src https://youtube.com` would enable embedding videos from YouTube but not from other origins. Use this in place of the deprecated **frame-src** directive.
- **connect-src** limits the origins to which you can connect (via XHR, WebSockets, and EventSource).
- **font-src** specifies the origins that can serve web fonts. Google’s Web Fonts could be enabled via `font-src https://themes.googleusercontent.com`
- **form-action** lists valid endpoints for submission from `<form>` tags.
- **frame-ancestors** specifies the sources that can embed the current page. This directive applies to `<frame>`, `<iframe>`, `<embed>`, and `<applet>`tags. This directive can’t be used in `<meta>` tags and applies only to non-HTML resources.
- **frame-src** deprecated. Use **child-src** instead.
- **img-src** defines the origins from which images can be loaded.
- **media-src** restricts the origins allowed to deliver video and audio.
- **object-src** allows control over Flash and other plugins.
- **plugin-types** limits the kinds of plugins a page may invoke.
- **report-uri** specifies a URL where a browser will send reports when a content security policy is violated. This directive can’t be used in `<meta>`tags.
- **style-src** is `script-src`’s counterpart for stylesheets.
- **upgrade-insecure-requests** Instructs user agents to rewrite URL schemes, changing HTTP to HTTPS. This directive is for web sites with large numbers of old URLs that need to be rewritten.