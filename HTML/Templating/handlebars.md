## Handlesbars

- logicless, you dont write logic
- Handlebar is a kind of mustache
- extensible with helpers instead of functions
- precompilation for performance

### Installation

https://handlebarsjs.com/installation.html

### Usage

- Get template content
- render template
- put html back in document

```js
$("document").ready(function() {
    var template = $("#itemTemplate").html();
    // Handlebars compiles the template into a callable function
    var renderer = Handlebars.compile(template);

    // call the compiled function with the template data
    var result = renderer({
        "item" : "Whisper 4000 in-home heater and dog walker",
        "description" : "Walk your dog and heat your house at the same time? Now you can, with the Whisper 4000 Home Heating system / Dog Treadmill!",
        "price" : 895.99,
        "inStock" : true,
        "quantity" : 100
    });

    $("#container").html(result);
});

```

### Each & If Else operator

To if you can pass anteing that can easily become true of falsey like boolean, array, string etc

```js
<script type="text/x-handlebars-template" id="itemTemplate">
    {{#each employees}}
         <div class="itemTemplateWrapper">
         {{! This is a handlebars comment and it is totally ignored }}
        <div>{{name}}</div>
        <div>{{title}}</div>
        <div>{{email}}</div>
        <div>{{phone}}</div>
        {{#if fulltime}}
        	 <div>Full-time employee</div>
         {{else}}
       		 <div>Part-time employee</div>
        {{/if}}
         </div>
     {{/each}}
</script>
```



### Helpers

Encapsulate functionality

```js
Handlebars.registerHelper("prodQuantity", function (prodData) {
                if (prodData.quantity >= 100)
                  return "We currently have a large amount in stock.";
                else
                  return "Hurry! We don't have many left in stock";    
            });
```

```html
<script type="text/x-handlebars-template" id="itemTemplate">
	<div>{{prodQuantity data}}</div>
</script>
```

### Precompilation

Get handlebars command by npm install -g handlebars

Creat.handlebars that just contains the template

Should use runtime code because precompied so smaller size

DOnt need to do compile ddddddd