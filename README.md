### peek-stream
---
https://github.com/mafintosh/peek-stream

```
npm install peek-stream
```

```js
var peek = require('peek-stream')
var ldjson = require('ldjson-stream')
var csv = require('csv-parser')
var isCSV = function(data){
  return data.toString().indexOf(',') > -1
}
var isJSON = function(data){
  try{
    JSON.parse(data)
    return true
  } catch(err){
  return false  
  }
}
var parser = function(){
  return peek(function(data, swap){
    if(isJSON(data)) return swap(null, ldjson())
    if(isCSV(data)) return swap(null, csv())
    swap(new Error('No parser available'))
  })
}

var parse = parser()
parse.write('{"hello":"world"}\n{"hello":"another"}\n')
parse.on('data', function(data){
  console.log(data)
})

var parse = parser()
parse.write('test,header\nvalue-1,value-2\n')
parse.on('data', function(data){
  console.log(data)
})

var parse = peek({
  maxBuffer: 10000
}, function(data, swap){
})
```

```
```


