#  Forms

#### Form tag

- GET sends data in URL: processform.php?fullname=.....
- POST gets data in backgournd and use for longer forms/secure
```html
<form action="wher to send data"
  enctype="how to encode data" //default
  method="post" >
  <input type="submit" value="OK">
  </form>
```
#### Enc Types
- `multipart/form-data` needed to get files
- `application/x-www-form-urlencoded` standard

## INPUT
```html
<label for="name">Name:</label>
<input name="user_name" id="name">
```

#### Basic Attributes

- name for form identification
- value is initial field value
- id is for js/`label for`

#### Input Types (text default)

- type = "password"
- type = "file"
- type = "checkbox"
- type= "radio"
- type="hidden" //just to send to your server
- type="submit"
- type="reset"
- type="image" //will submit, to make submit button image
- type="number"


#### Advanced Forms
Values are sent to the sever
Multiple lets you select multiple, sends csv
```html
<textarea name="longertext"> prefileld </textarea>
<select [multiple] name="myoptions">
  <option> Choose .. </option>
  <option value="valueToGiveName" > Label 1 </option>
  <option value="b" > Label 2 </option>
</select>
```

## Submit

```html
<div class="button">
  <button type="submit">Send your message</button>
</div>
```

## Events

```js
document.forms.theactualformid.myname.onfocus = () => {
  //do stuff when you on thing
}
document.forms.theactualformid.onblur = () => {
  //do stuff when you leave thing: hints?, fill me out
}

document.forms.theactualformid.onchange=() => {
  var theURL = document.theform.myurl.value;
  // do validation
}
```

* onsubmit *
Good way to do validation is have dictionary with key being name and having required, placeholder, and pattern that you can check dynamically
```js
document.forms.theactualformid.onsubmit = () => {
  //do validation
  //do ajax
  return false; //prevent form from submitting
};


$(document).ready(function(){
  $("#eventCreation").submit(function( event ) {
    alert( "Handler for .submit() called." );
    rawFormData = $( this ).serializeArray();
    event.preventDefault();
  });
});
```


## HTML5
Doesn't work in older browser(date doesn't work with safari)
Mobile can change keyboard accordingly
Older browsers will show text field
https://www.caniuse.com/

#### Advanced Stuff
Can do multiple in email and files

- type="date"
- type="color"
- type="range"

*Attributes:*
- multiple
- autocomplete //great for password managers and recommended by Chrome
  - "username" | "current-password" | "new-password"
- placeholder="Enter first name"
- required //will stop if not there
- pattern //can do regular expression validation
- maxlength='10'
- min='10'
- min='2013-03-04'
- max='40'

##### MIME TYPE
MIME is multipurpose internal mail extensions
Type like image, audio, or video then subtype like jpeg

*Attributes:*
- accept="image/png"
- accept="image/\*" //select all images

#### Input Validation
- type="email"
- type="url"
- type="number"
