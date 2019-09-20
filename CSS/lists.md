# Lists

You can style many parts of the list

```css
  list-style-image: url('sqpurple.gif');
  list-style-position: inside; //default is outside

```

List also comes with default margin and padding if you want to get rid of it

```css
ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
}
```

You can't change the size of the image very well so usually just better to use an actual img tag

### Getting that last/first element to be properly spaced

```scss
.article-list {
  margin-bottom: 1rem;
  
  &:last-child {
    margin-bottom: 0;
  }
}
```

