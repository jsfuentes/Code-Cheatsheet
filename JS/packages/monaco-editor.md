## [Monaco Editor](https://microsoft.github.io/monaco-editor/api/index.html)

The open source tool behind VSCode with both editor and diff editor

monaco can create multiple editors that share models

[React version](https://github.com/react-monaco-editor/react-moaco-editor)

```js
      <MonacoEditor
        width="100%"
        height={height}
        language="javascript"
        theme="vs-dark"
        // @ts-ignore the wordWrap props is giving an error, but working properly
        options={options}
        editorDidMount={editorDidMount}
        defaultValue="//Loading..."
        // onChange={onChange} //of current model
      />
```

Use [webpack plugin](https://github.com/Microsoft/monaco-editor-webpack-plugin#options)

`languages` () - include only a subset of the languages supported.string[]default value: 

['apex', 'azcli', 'bat', 'clojure', 'coffee', 'cpp', 'csharp', 'csp', 'css', 'dockerfile', 'fsharp', 'go', 'handlebars', 'html', 'ini', 'java', 'javascript', 'json', 'less', 'lua', 'markdown', 'msdax', 'mysql', 'objective', 'perl', 'pgsql', 'php', 'postiats', 'powerquery', 'powershell', 'pug', 'python', 'r', 'razor', 'redis', 'redshift', 'ruby', 'rust', 'sb', 'scheme', 'scss', 'shell', 'solidity', 'sql', 'st', 'swift', 'typescript', 'vb', 'xml', 'yaml'].