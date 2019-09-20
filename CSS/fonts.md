# Fonts

#### Font-weight

normal | bold => equivalent of 400 | 700

lighter | bolder => compared to inherited font weight

100 | 200 | 300 | 400 | 500 | 600 | 700 | 800 | 900

## Custom Fonts

1) Get the font file

2) You need at least the woff2 and off, [fontsquirrel helps](https://www.fontsquirrel.com/tools/webfont-generator)

3) Add the font file to your static website folder

4) Add the following to your html somehow

```css
@font-face {
    font-family: 'wremenabold';
    src: url('app/static/webfontkit-WremenaBold/wremena_bold-webfont.woff2') format('woff2'),
        url('app/static/webfontkit-WremenaBold/wremena_bold-webfont.woff') format('woff');
    font-weight: normal;
    font-style: normal;
}
```

If you are using scss, you need to only include it once(no variables import to every file) since the url route is a file path

