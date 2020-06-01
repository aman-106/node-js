# node-js
node js is async event driven and meant for scalable  network applications.
light-weight 

https://github.com/jscomplete/ngs
https://github.com/jscomplete/advanced-nodejs
https://medium.com/edge-coders/how-well-do-you-know-node-js-36b1473c01c8

## uses
node js for microservivces and api -- js code and node env works as server
serverless cloud -- like async function act as sever response 
command line application -- like webpack  , 
desktop applications - like electron js

## REPL
read eval print loop

https://github.com/jscomplete/ngs

## what makes node js 
V8 engine
libuv - event loop , async IO
project spefic code
npm - package manager
commonJs - module dependency manager

-- no polyfills 
-- but node js version 
-- os dependent 
## not good fit
cpu computattion intensive


  ### Node Event Loop

process per client -- one process handles a resquest, indepentent of one other.
thread per cleint -- one thread handle a request ( concurrent threads for clieent ) multi thread


"Siingle THread" -- via under hood multi thread.
one function at one time , 
like cook - waiter -- dinners 
 acting some db tasks --function --- requests 
 function should as minium time to server request and server next.
  
  https://github.com/pofallon/nodejs-big-picture/blob/master/callbacks/customer.js
  
  ### async 
  passing callback error , data 
  async pattern 
  callback hell
  promises or async/await 
  
   node api and event emitters
   utils.promisfy
   
   
   ### Streams
   readable stream 
   writable stream 
   duplex (write and read ) stream 
   
   
   Streams have events , methods and properties
   
   handling backPresurre (one stream process faster than other )
   
   piping streams 
   eg 
   read a file -> pipe -> write to http resposne
   
   ## Modulazing ur App
   npm and modules
   npm - cli and command line
   
   ## assemlby a node js 
   setup 
   testing - bdd
   mocha test 
   chai assertion lib
   sinon - mocks things
   
   debugging - node inspect file.js
                using vsc extensions
                
## setInterval , setTimeOut
```js
id = setInterval(func,ms,paramsForFunc)
```

ms -- is not exact time but not miniium time after blocking exuction is done.
setINterval excutes after every ms , clearInterval(id) to clear.


## Process
process has event emits  , only sync code can be excuted 
methods -exit
```js
process.on('exit',function(code){
    console.log('error'+code)
})
process.on('uncaughtException',function(){
    // got exception
    process.exit(1);
})

```
process.env
process.argv
// interface btw the node and os - streams

process.stdin
process.stdout
process.stderr
process.exit -- function

Instead of dircetly process.env.PORT we can utils file for confriguration 
utils.js
```js
export default const utils ={
    PORT:process.env.PORT || 3000,
}
```
```js
process.stdin.on('readable', () => {
  const chunk = process.stdin.read();
  if (chunk !== null) {
    process.stdout.write(chunk);
  }
});
//OR 
process.stdin.pipe(process.stdout);
```


## Modules
file or folder containing a code

node wraps a file in function

```js
console.log(arguments);

```

it equilavent to 
```js
function nodejsWrapper(exports,module,require__filename,__driname){ // commonJS module
    // file code here
    // dy default exports = {}
    // exports is alias to module.exports
    //  exports.a=3 is cool but exports = ()=>{} not ok
    // so to return function exports api , use module.exports = ()=>{};
    // bascilly mutation on exports is cool but re assgin is not ok
    
    return module.exports // by default
}
```

varibale defined in file , browser - global varible but for nodejs is local varibale.


## Node Global Object
```js

console.dir(global,{depth:0})

// { console: [Getter],
//   DTRACE_NET_SERVER_CONNECTION: [Function],
//   DTRACE_NET_STREAM_END: [Function],
//   DTRACE_HTTP_SERVER_REQUEST: [Function],
//   DTRACE_HTTP_SERVER_RESPONSE: [Function],
//   DTRACE_HTTP_CLIENT_REQUEST: [Function],
//   DTRACE_HTTP_CLIENT_RESPONSE: [Function],
//   global: [Circular],
//   process: [Object],
//   Buffer: [Object],
//   clearImmediate: [Function],
//   clearInterval: [Function],
//   clearTimeout: [Function],
//   setImmediate: [Object],
//   setInterval: [Function],
//   setTimeout: [Object] }


globale.ans = 383; //bad

// dont use global variables 
```

## Event Loop
handle async actions and interface so dont have deal with threads


## Errors vs Execption
error is problem
exceptiion is condition or account for error

```js

try{
    // some code here
}catch(err){
        console.log('The generic err trap')
}
    
try{
    // some code here
}catch(err){
    if(err.code=="ENOENT){
        console.log('File not found')
    }else{
        console.log('The generic err trap'); // shows  unknown error
        throw err;
    }
}   
```

## Node clusters
production app run with cluster of nodes
 use full capcity server cpu 
 in case of error , mointor the error in node
 
 eg epm2
 
 ## Node async patterns
 callback pattern --- callback hell
 promoise , using async await function - util.primosify , 
 
 ```js
 const fs = require('fs');
 const readFile = util.promisify(fs.readFile);
 // or native support for promise 
 const { readFile } = require('fs').promises;
 ```
 
 ## Eevnt Emitters
 
  Subscription shoud be before emitting the event .
  Below code wont fire any events or should be delayed .
  
  allows different modules to work  without dependices
  
  ```js
  const e = new Events();
  e.emit('my-event'); // emit
  e.on('my-event', ()=>{  // subscription
  // to something
  })  
  
 // Streams are Event Emitters
// process.stdin, process.stdout
```
## fs 
fs.

## working with web servers

using htttp module
```js
const http = require('http');

const server = http.createServer((req, res) => {
  res.end('Hello World\n');
  // or 
  res.write('dkdkd');
  res.end();
});

server.listen(4242, () => {
  console.log('Server is running...');
});

```
both request and resposne are stream and have events for different functiions
class for 
Request -  IncommingMessage // as a server
Resposne - ServerResponse 

htttp.clientRequest for request to http server

## Operating System
read and write to os

### Os

```js
const os = require('os');

console.log('OS platform:', os.platform());

console.log('OS CPU architecture:', os.arch());

console.log('# of logical CPU cores', os.cpus().length);

console.log('Home directory for current user', os.homedir());

console.log('line 1' + os.EOL + 'line 2' + os.EOL + 'line 3');
```

## fs 
https://nodejs.org/api/fs.html
readFile -- path , format , callback 

if **format** is missing ,
    callback(err,**buffer**)=>{}
else 
    callback(err,data)=>{}
    
```js

  readFile(path[, options])
  createReadStream(path[, options])

  writeFile(file, data[, options])
  
  ```
  
## Child Process
  tot create sub process in OS and use result when it is done
  
```js
const { spawn } = require('child_process');

// Print Working Directory
const pwd = spawn('pwd');
pwd.stdout.pipe(process.stdout);

// Read content of a file
const { HOME } = process.env;
const cat = spawn('cat', [`${HOME}/.bash_profile`]);
cat.stdout.pipe(process.stdout);

// List files
const ls = spawn('ls', ['-l', '.']);
ls.stdout.pipe(process.stdout);

// Use Shell Syntax
const shell = spawn('ls -al ~ | wc -l', { shell: true });
shell.stdout.pipe(process.stdout);
```

###  Node debugging


```js
node --inspect-brk filename.js

 // open 
// chrome://inspect 
// for debug mode for filename
// see code wrapped in function  like console.log(arguments) will be works
```


# Node adanced topics

## Node architect ure -- VM (V8) and libuv

node -v8-options | grep "in progess"

v8 features - shipping , in progess and staged
staged can be used by --harmony

over view model of node js
https://medium.com/@chathuranga94/nodejs-architecture-concurrency-model-f71da5f53d1d


## Buffer 
Buffer class is a subclass of the Uint8Array class
used for binary stream of data .
chuch of memory allocated outside V8 Heap and we put some data in that memory and that data can be interpated in different ways
 so charcter encoding needed for buffer.
 
 Buffer is low level sequnce of binary data 
 Buffer is allocated , cant be resized .
 
 \u0000 --  unicode null character.
 ```js 
 b = Buffer.allocUnsafe(800); // alloc existing 800 bytes of memory , which refs to previous used bytes
  a= Buffer.alloc(800) //
  
 const string = 'touch';
const buffer = Buffer.from('touch');
// string.length, buffer.length
5 5 

const string = 'touché';
const buffer = Buffer.from('touché'); // utf-8 encoding doesnt have this special char
6 7 
 ```
 
 useful reading img file , compzressed file
 
 https://nodejs.org/api/buffer.html#buffer_buf_slice_start_end
 
 orginail_memory_reference = buffer.slice(start , end)
 **new Buffer that references the same memory as the original, but offset and cropped by the start and end indices.**
 
 
 ```js
 
   let tag = buffer.slice(-4, -1); // contains last three bits 
// TAG IS MEMEORY REFERNCE OR POINTER FOR 3 Byte FROM MEMORY IN BUFFER 
  for(let i=0;i < tag.length; i++) {
    tag[i] = '\u000';
  }
  
  // CHANGINg TAG will be last 3 Byte in buffer 
  
  ```
  
  
  when converting streams of binary data into , we should use string_decoder module 
 
 The string_decoder module provides an API for decoding Buffer objects into strings in a manner that preserves encoded multi-byte UTF-8 and UTF-16 characters. It can be accessed using:
 
 https://nodejs.org/api/string_decoder.html
 
 
 ```js
 const { StringDecoder } = require('string_decoder');
const decoder = new StringDecoder('utf8');

process.stdin.on('readable', () => {
  const chunk = process.stdin.read();
  if (chunk != null) {
    const buffer = Buffer.from([chunk]);
    console.log('With .toString():', buffer.toString());
    console.log('With StringDecoder:', decoder.write(buffer));
  }
});
```
 
 
 ## how require works ?
 module --global object 
 
 require  -- global function to acesss modules
 
 require('file-some')
 
 module --
 gives info on file like
 {
     id,
     filename,
     paths,
     loaded,
 }
 
 node js looks for file in paths of modules unitl root folder exception for core modules
 
 
 require resolve teh file and excute 
 but only resolve the module 
 
 
 require.resolve can be used for ONLY resolving not excuting.
 require.resolve stils error if file doesnt exists.
 used for checking package is installed or not
  
  
  module can be folder with index.js and can be resolved using the require .
  
  
  
  
  package json main property to set index file eg 
  ```js
  {
      name:'find-me',
      main:'start.js',
  }
  
  ```
 
 
 
 
 
 
 











                 
   
   
   
   
    
 



