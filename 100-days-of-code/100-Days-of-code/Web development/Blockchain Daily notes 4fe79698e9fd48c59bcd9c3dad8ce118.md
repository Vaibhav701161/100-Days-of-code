- DAY 1 ( 11th JULY , 2024)
    - Call stack:  Learned how multiple functions are executed using the concept of call stack.
    
    ```jsx
    fnction hello (){
    console.log("hello fxn is being executed")
    }
    function demo(){
    console.log("demo fxn is being executed")
    hello();
    }
    demo();
    console.log("bye!")
    
    ```
    
    - Callback hell: when multiple callbacks are nested together.;
    
    in this code, first : demo is being executed — hello is being executed — bye!
    
    ```jsx
    h1 = document.querySelector="h1";
    function changeColor(color, delay  , nextColorChange){
    setTimeOut(()=>{
    h1.style.color   = color;
    if (nextColorChange) nextcolorChange(()=>
    delay();
    });
    )};
    
    changeColor("red",1000 () =>{
    changeColor("blue",1000 () => {
    changeColor("green",1000 () => {
    changeColor("brown",1000 );
    )};
    )};
    )};
    
    ```
    
    - Promises: used to get rid of call back hell!
    - It is an object in JavaScript which represents the eventual completion (or  failure) of an asynchronous operation.
    
    ```jsx
    function saveToDb(data){
    return new promise ((resolve,reject)=>{
    let internetSpeed =math.floor(mth.random())*4  ;
    	if (internetSpeed > 4){
    	resolve: ("success! : data was saved");
    	}
    	else{
    	reject:("data wasn't saved!")
    	};
    });
    };
    ```
    
    - Promises have there own methods out of which the most famous one is then() and catch() method.
    - They work according to the state of the promise —  if promise is fulfilled, .then() method can be used ,  if rejected , .catch() method can be used.
    
    ```jsx
    let request =  saveToDbPromise("apnacollege");
    request
    .then(()=>{
    console.log("promise is resolved!");
    });
    .catch(()=>{
    console.log("promise is rejected");
    });/
    ```
    
    - Promise chaining : Improved version of promises! (kind of similar to switch case!)
    
    ```jsx
    let request =  saveToDbPromise("apnacollege");
    request
    .then(()=>{
    console.log("promise1 is resolved!");
    return  saveToDbPromise("hello world")
    });
    .then(()=>{
    console.log("promise2 is resolved!");
    });
    .then(()=>{
    console.log("promise3 is resolved!");
    });
    .catch(()=>{
    console.log("some promise is rejected");
    });
    ```
    
    - Result and Errors : By default in promises, we can take argument result in .then() and error argument in .catch() method.
    
    ```jsx
    let request =  saveToDbPromise("apnacollege");
    request
    .then((result)=>{
    console.log("result : ",result);
    console.log("promise is resolved!");
    });
    .catch((error)=>{
    console.log("error: ",error);
    console.log("promise is rejected");
    });
    ```
    
    - Async : returns a promise.
    
    ```jsx
    async function greet(){
    console.log("hello world");
    };
    
    greet()
    .then((result)=>{
    console.log("result : ",result);
    console.log("promise is resolved!");
    });
    .catch((err)=>{
    console.log("error: ",err);
    console.log("promise is rejected");
    });
    ```
    
    - Await : Pauses the execution of it’s surrounding async  function until the promise is settled.
    
    ```jsx
    async function show(){
    
    await colorChange("voilet",1000);
    await colorChange("red",1000);
    await colorChange("blue",1000);
    await colorChange("green",1000);
    await colorChange("yellow",1000);
    await colorChange("purple",1000);
    
    return "done";
    }
    ```
    
    - API - (Application programming interface) : We as users never  access servers directly. We access the server APIs for the  desired data to be fetched.
    - The data returned by the APIs is in a special format called JSON.
 
  
# DAY-2
### TERMINAL COMMANDS!

- ls : List files
- pwd: print working directory (where am I)
- clear: clear screen
- cd : change directory
- cd .. : to get one step back!
- mkdir: make directory : makes only directory not files!
- Touch command : used to create files! ex: touch index.html
- rm : remove files
- rmdir: removes empty files
- rm -rf: remove any files

### GITHUB COMMANDS!

- git clone ←  some link → : cloning a repo on your local machine.
- git status: displays the status of the code
- git add ← file name → : adds new or changed files in your working directory to get git staging area
- git commit -m “some message”: it is the record of change
- git  push origin main : upload the local repo content to remote repo
- Git init :  used to create a new github repo
- git remote add origin ← link →
- git remote -v : verify remote
- git branch: to check branch
- git branch -M main : to rename branch
- git push origin main
- git checkout ← branch name → : to navigate
- git checkout -b ← new branch name →  : to create new branch
- git branch -d ← branch name → : to delete branch
- git merge ← branch name →: to merge two branches
- git reset ←file name → : the reset unwanted staged files

## NODE.JS

- It is a JavaScript runtime environment.
- `process.argv` is a special array that holds the command-line arguments you pass when you run a Node.js script.
- Module.exports: if we had made multiple files and we want to export the function of one file to another to save time , we use
- require() :  used to receive the info of the file which is exporting data.

```jsx
// math.js file exporting data
module.exports = 123;
```

```jsx
// app.js file recieving it 
const someValue = require("./math");
```

- if we had to export data from  a folder/ directory, the first step is that we make a new index.js file in that directory.
- we will receive all the info in that file.
- then we will make an array including all the values we want.
- then we will export that array.

ex: data/file1.js:

```jsx
const value1 = " value from value 1"
module.exports = value1;
```

data/file2.js:

```jsx
const value2 = "Value from file2";
module.exports = value2;
```

```jsx
// index.html file
const value1 = require('./file1');
const value2 = require("./value2");

const valuesArray = [vale1,value2];
module.exports = valuesArray;
```

- Package.json = contains descriptive and functional metadata about a project, such as name, version and dependencies.
- npm init : this command is  used to initialize package.json
- Export : we can asynchronously import data .

```jsx
function add(x, y) {
  return x + y;
}

export default add;  // This exports the function as the default export

```

```jsx
import add from './math.js';  // Imports the default export from math.js

const result = add(5, 3);
console.log(result); // Output: 8

```
