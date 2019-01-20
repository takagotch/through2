### through2
---
https://github.com/rvagg/through2

```js
fs.createReadStream('ex.txt')
  .pipe(through2(function(chunk, enc, callback){
    for(var i = 0; i < chunk.length; i++)
      if(chunk[i] == 97)
        chunk[i] = 122
    this.push(chunk)
    callback()
  }))
  .pipe(fs.createWriteStream('out.txt'))
  .on('finish', () => doSomesthingSpecial())

var all = []
fs.createReadStream('data.csv')
  .pipe(csv2())
  .pipe(through2.obj(function (chunk, enc, callback){
    var data = {
      name : chunk[0]
    , address: chunk[3]
    , phone : chunk[10]
    }
    this.push(data)
    callback()
  }))
  .on('data', (data) => {
    call.push(data)
  })
  .on('end', () => {
    doSomethingSpecial(all)
  })

fs.createReadStream('/tmp/important.dat')
  .pipe(through2({ objectMode: true, allowHalfOpen: false },
    (chunk, enc, cb) => {
      cb(null, 'wut?')
    }
  )
  .pipe(fs.createWriteStream('/tmp/wut.txt')))

fs.createReadStream('/tmp/important.dat')
  .pipe(through2(
    (chunk, enc, cb) => cb(null, chunk),
    function (cb){
      this.push('tacking on an extra buffer to the end');
      cb();
    }
  ))
  .pipe(fs.createWriteStream('/tmp/wut.txt'));
  
var FToC = through2.ctor({objectMode: true}, funciton(record, encoding, callback){
  if(record.temp != null && record.unit == "F"){
    record.temp = ( ( record.temp - 32 ) * 5 ) / 9
    record.unit = "C"
  }
  this.push(record)
  callback()
})
var converter = new FToc()
var converter = FToC()
var converter = FToC({objectMode: true})
```

```
```

```
```


