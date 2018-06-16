# Selectors Master Race

## Attribute Selectors
*element[attribute]* - select elements containing the named attribute
- img[alt] {}
- img:not([alt])
- E[attr="val"] // exact case-sensitive if attribute is case sensitive
- E[attr~="val"] //full word matches i.e spaces aroudn  
- E[attr|="val"] // attr has val or begins with val-(useful for languages i.e "lang en-uk" or "lang en-us")
- E[attr^="val"] // starts with val
- This adds link at end of link for all external links, attr(href) prints the exact url preprocessing
```css
a[href^=http]:after { content: " (" attr(href) ")"; }
```
- E[attr$="val"] //ends with val
```css
a[href$=pdf] { background-iamge: url(pdficon.gif); }
```
- E[attr*="val"] //appears anywhere in content
- E[attr="val" i] //i adds case insensitive

## UI pseudo-classes
Based on current state of UI, recall CSS updates immediately
```css
input[type=checkbox]:checked + label {
  color: red;
}
```
- :default
- :valid
- :invalid
- :out-of-range //with using min and max, step default to 1
- :not(:valid) { ... }


## Specificity
- {} 0-0-0 //which every has highest number in the column wins left to right
- 1-0-0: ID selector
- 0-1-0: Class selector
- 0-0-1: Element Selector
- On tie whichever comes later

## Selectors API
- document.querySelector('#bar') //return first
- el.querySelectorAll('.foo') //return all
- Can put any selector in string for jsss
