# Csv

```sh
 npm i -s csv-parser
```

Then, lets put the CSV data from the beginning of the article to a file called "data.csv" and follow up with a very simple example:

```javascript
const csv = require('csv-parser');
const fs = require('fs');

fs.createReadStream('data.csv')
  .pipe(csv())
  .on('data', (row) => {
    console.log(row);
  })
  .on('end', () => {
    console.log('CSV file successfully processed');
  });
```

