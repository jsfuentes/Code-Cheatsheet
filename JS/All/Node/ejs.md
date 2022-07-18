# ejs Templating

## Basics
`<% [code here] %>`

## Partials
 Under the views/partials/ directory create a file called footer.ejs
 `<%- include('partials/footer') %>`

## IF
```js
 <% if (user) { %>
   <h2><%= user.name %></h2>
 <% } %>
 ```

## Loop
```js
<% users.forEach(function(user){ %>
    <%- include('user/show', {user: user}); %>
  <% });
%>
```

## Tags
<% 'Scriptlet' tag, for control-flow, no output
<%_ ‘Whitespace Slurping’ Scriptlet tag, strips all whitespace before it
<%= Outputs the value into the template (HTML escaped)
<%- Outputs the unescaped value into the template
<%# Comment tag, no execution, no output
<%% Outputs a literal '<%'
%> Plain ending tag
-%> Trim-mode ('newline slurp') tag, trims following newline
_%> ‘Whitespace Slurping’ ending tag, removes all whitespace after it
