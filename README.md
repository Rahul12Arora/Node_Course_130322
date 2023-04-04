# Node_Course_130322
Learning Node

<h2>Intro:</h2>

Node.js is an open-source, cross-platform, back-end JavaScript runtime environment that allows developers to build server-side applications using JavaScript. In simple terms, it lets you write server-side code using JavaScript, the same language used for front-end development.</br>

One of the biggest advantages of Node.js is its ability to handle a large number of concurrent connections with low overhead. This makes it a popular choice for building real-time, high-traffic applications such as chat applications, online gaming platforms, and social media sites.</br>

Node.js is also known for its event-driven, non-blocking I/O model, which allows it to handle asynchronous operations efficiently. This means that Node.js can handle multiple tasks simultaneously without getting bogged down, making it a good choice for building scalable applications.</br>

Note - nodemon is a tool that helps develop Node.js based applications by automatically restarting the node application when file changes in the directory are detected.</br>
Note - npm run myscriptname</br>
Note- event queues takes in alot of operations at once, node is based on concept of non-blocking async operations but it can still be blocked by a sync blocking operation.</br>

<h2>Start:</h2>

1.) Run 'npm init' to create a package.json file.

<h3>package.json && 'npm install'</h3>

The purpose of package.json is to have an Object containing details of all dependencies we installed from NPM as packages, So that the next time we open our code in another computer, we run 'npm install' and that command installs all the dependencies from the package.json into that computer. Everything we install comes from "registery.npmjs.org"
For eg: 'npm install uuid' is a package that we can install to generate random ids, Now my package.json file automatically has the details of this dependency like version number;

<h3>'npm install -D nodemon'</h3>

Nodemon is a tool used in Node.js development that automatically restarts the Node.js application whenever changes are made to the code. This helps developers save time and effort by eliminating the need to manually stop and restart the server every time a code change is made.

<h2>Export & import</h2>

creating & exporting functions,objects,classes,etc, from other js file

<h3>Export</h3>

```
// In a math.js file:
function add(a, b) {
  return a + b;
}

function sub(a, b) {
  return a - b;
}

function mul(a, b) {
  return a * b;
}

function div(a, b) {
  return a / b;
}

module.exports = {
  add: add,
  sub: sub,
  mul: mul,
  div: div,
};
-----------------------
// exports.add = add;
// exports.sub = sub;
// exports.mul = mul;
// exports.div = div;

---------------------------------------------------------------------------------------------------
export function add(a, b) {
  return a + b;
}

export default function multiply(a, b) {
  return a * b;
}
```

<h3>Import</h3>

```
// In another file where you want to use these functions:
const math = require('./math.js');
console.log(math.add(2, 3)); // Output: 5
console.log(math.mul(4, 5)); // Output: 20
---------------------------------------------------
const myFunction = require('./myModule.js').default;

console.log(myFunction(2, 3)); // Output: 6

------------------------------------------------------------------------------------------------------

ES6 WAY

import multiply, { add, subtract } from './math.js';
//multiply is the default export from math.js file; add & subtract is simple export
```

option2

```
const person = {
    name: 'John Doe',
    age: 30
}

module.exports = person;
exports.person=person;            //this is also valid

//wrong way
exports = {person:person}  // we need to export to module.exports, creating a new exports file will create a completely new exports object that will not function as expected

or
exporting classes in this manner
class Car {
  constructor(make, model, year) {
    this.make = make;
    this.model = model;
    this.year = year;
  }

  getAge() {
    return new Date().getFullYear() - this.year;
  }
}

module.exports = Car;
```


<h3>importing the above in another js file</h3>

```
const person = require('./person');
console.log(person.name);

or

const Car = require(./car);    //name of the file
const myCar = new Car('Toyota', 'Camry', 2018);
console.log(myCar.name)
```

<h2>Function Wrapper in Node.js files</h2>

In Node.js, a function wrapper is a piece of code that surrounds a module's code and provides a layer of abstraction between the module and the rest of the application. It is typically used to wrap the module code inside a function, allowing the module to have its own scope and avoid conflicts with other modules.

Here's an example of a function wrapper in Node.js:
```
(function(exports, require, module, __filename, __dirname) {
  // Module code goes here
  function greet(name) {
    console.log(`Hello, ${name}!`);
  }

  // Expose the greet function as a module
  module.exports = greet;
});
```

<h2>Core modules can be imoprted as follows</h2>
<h3>core modules are already included with node so we don't have to install them</h3>

**path is a module that tells us the file name & directory name**

```
const path = require('path');
```

**File System Module (fs) lets us create files/folders & write, override, join & append data**

```
const fs = require('fs');
const fs = require('fs').promises;  //promises version so we can use .then()

fs.mkdir('test123',(err)=>{       //async module code
if (err) throw err;
console.log( "Folder created" );
});

console.log("test")               //sync
//output => test
            Folder created

# more on this

fs.mkdir('test123')
.then(() => {console.log('folder created')})
.catch((err) => {console.log(err)})

fs.watch('test123/test.txt').then((event, filename) => {console.log(event, filename)})

fs.writeFile('test123/test.txt', 'Hello World').then(() => {console.log('file created')})
.catch((err) => {console.log(err)})

fs.readFile('test123/test.txt', (err,data) => {console.log(data);})

fs.appendFile('test123/test.txt', 'this will append ? ')

try {
const value = fs.readFileSync('test123/tesere.txt', 'utf8')}
catch (err) {
console.log(err)
console.log('code is running')
}
console.log('end of code');
```

<h3>28032023</h3>
**os module gives us infor about os**


```
const os = require('os');

values of os.platform()
// darwin (macOS)
// freebsd (FreeBSD)
// linux (Linux)
// sunos (SunOS)
// win32 (Windows)

if(os.platform() === 'win32'){
console.log("Windows");
}

os.cpus().forEach((cpu, index) => {
console.log(`CPU ${index} : ${cpu.model}`);
})
console.log(os.arch()); //architecture
console.log(os.freemem()); //free memory
console.log(os.networkInterfaces()); //total memory
```

```
const EventEmitter = require('events');

class ExamOverEventEmitter extends EventEmitter {}

const examOver = new ExamOverEventEmitter();

examOver.on('examOver', () => {console.log('exam is over says student 1');})

examOver.on('examStarts', () => {console.log('exam is over says student 2');})

examOver.emit('examOver');

examOver.emit('examOver');
```

