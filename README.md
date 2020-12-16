<a href="https://covid19datahub.io"><img src="https://storage.covid19datahub.io/logo.svg" align="right" height="128"/></a>

# Node.js Interface to COVID-19 Data Hub
[![DOI](https://joss.theoj.org/papers/10.21105/joss.02376/status.svg)](https://doi.org/10.21105/joss.02376)

Libraries [axios](https://www.npmjs.com/package/axios) (for online data fetching) and [csv-parse](https://www.npmjs.com/package/csv-parse) (for csv parsing). Install them by

```bash
npm i axios csv-parse
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
