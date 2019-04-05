# Script

`npm install react-load-script`

Allow you to easily load 3rd party scripts into app when needed

## API

The package exports a single component with the following props:

#### `onCreate`

Called as soon as the script tag is created.

#### `onError` (required)

Called in case of an error with the script.

#### `onLoad` (required)

Called when the requested script is fully loaded.

#### `url` (required)

URL pointing to the script you want to load.

#### `attributes`

An object used to define custom attributes to be set on the script element. For example, `attributes={{ id: 'someId', 'data-custom: 'value' }}` will result in `<script id="someId" data-custom="value" />`

## Example

```javascript
import Script from 'react-load-script'
 
render() {
  return (
    <Script
      url="https://ajax.googleapis.com/ajax/libs/jquery/1.8.3/jquery.min.js"
      onCreate={this.handleScriptCreate.bind(this)}
      onError={this.handleScriptError.bind(this)}
      onLoad={this.handleScriptLoad.bind(this)}
    />
  )
}
```