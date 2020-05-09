# node-js
node js is async event driven and meant for scalable  network applications.
light-weight 

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


##process
process.env
process.argv
// interface btw the node and os - streams
process.stdin
process.stdout
process.stderr
process.exit -- function
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
 promoise - util.primosify , 
 
 ```js
 const fs = require('fs');
 const readFile = util.promisify(fs.readFile);
 // or native support for promise 
 const { readFile } = require('fs').promises;
 ```
 
 









                 
   
   
   
   
    
 



