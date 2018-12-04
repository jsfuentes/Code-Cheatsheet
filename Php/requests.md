# Handling Requests with PHP

### Calling in HTML
```HTML
<form ... action="process.php" method=[GET/POST]>
```
- `GET` will link to page and pass in url
- `POST` will link to page and pass in request body

### Superglobals
- Variables \$\_GET \$\_POST, \$\_REQUEST, $\_COOKIE
- Request is a combo superglobal and gets get and post
- Test with `var_dump($_GET)`
- These are associative arrays so just use ['key'] to access

### Returning
- `echo`

## Submit to yourself
- Can make form submit to itself `action="<?php echo $_SERVER['PHP_SELF'] ?>"`
- Before processing do, `if(($\_SERVER['REQUEST_METHOD'] == 'POST') && (!empty($\_POST['action'])));`

### Validation
- if else preg_match, `preg_match('re', str)`

### Form Specifics
- Names must be different
- If you have like a checkbox with the same name, can make `name=music[]` which will make it an array
- echoing `echo checked` at the end of checkbox input tag will check box
