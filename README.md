# Node.js Interface to COVID-19 Data Hub

Libraries [axios](https://www.npmjs.com/package/axios) (for online data fetching) and [csv-parse](https://www.npmjs.com/package/csv-parse) (for csv parsing). Install them by

```bash
npm i -g axios csv-parse
```

Once installed, fetch the data:

```js
const axios = require('axios');
const parse = require('csv-parse/lib/sync')
const dataCOVID19 = async () => {
    // download
    let resp = await axios.get('https://storage.covid19datahub.io/data-1.csv')
    let data = unescape(resp.data)
    // parse
    return parse(data, {
        columns: true,
        skip_empty_lines: true
    })
}
// call
let dataPromise = dataCOVID19();
// set callback for data
dataPromise.then((results) => {
    for(r in results) {
        let result = results[r] 
        console.log(result)
    }
})
```
