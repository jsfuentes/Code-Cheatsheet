## Mustache

- logic-less, templating engine handles most, basic things like conditionals

- some advanced features like tags and functions

  ### Installing

  go to github repo and download: https://jquery.com/download/

  

  

### Rendering Template

- Get template content 
- render the template 
- put html back into document  

```js
$("document").ready(() => {
    var tlContent = $('#tmpID').html;
    var result = Mustache.render(tlContent, dataObj);
    containerElement.innerHTML.result;
});
```

```html
<script type="text/template" id="tmpID>
                                 
</script>
```

{{! This is a mustache comment and is totally ignore }}

### Sections and Conditions

Repeated data: Loop over all the employees and get each individual object

```js
var template = $("#itemTemplate").html();
var result = Mustache.render(template, {
               "employees" : [{
                  ......
                   
               }]);
            $("#container").html(result);

```



```html
<script type="text/template">
{{#employees}}
	<div> {{name}} </div>
    {{#inStock}}        
    <div><span>Quantity in stock: </span><span>{{quantity}}</span></div>
    {{/inStock}}
    {{^inStock}}
    <div><span>It appears we are out of stock on this item :-(</span></div>
    {{/inStock}}
{{/employees}}
</script>
```

### Functions

is the value of the field is actually a function, you can use like a property . Mustache will call it and this. will be set to the data object itself. 

What if we make a section with a function that takes a text and renders

