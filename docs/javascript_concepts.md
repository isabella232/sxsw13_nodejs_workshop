# Javascript Concepts

### functions, objects
Everything in Javascript can be considered an object in most real-world uses. Like most other languages, Javascript does have primitives (string, number, boolean), however in most use cases these will be converted as needed automatically by Javascript into their object counterparts. I’m not going to go into the details about primitives, just be aware they exist.

Unlike many languages, Functions are first-class objects and can be created, stored, and passed around the application like any other object. This includes being used as an argument in a function call, where you can pass another function into it. You can also add properties to a function just as you would with any other standard object. Functions can be thought of just like any other object, with the key difference being that you can execute them. This an important concept when we think about Javascript’s version of a Class, which is really just a function. We can then add additional functions onto them as properties, which then become the equivalent of a Class’s methods.


### scope
A new scope is created anytime a function is called. A variable's scope will either be local to that function or global. If the variable is not properly declared with the "var" keyword, it will be given global scope. Otherwise, it is given local function scope relative to the current execution. Block scope does not exist. If a variable is declared inside a block statement, the declaration will be hoisted to the top of the nearest function. Variables that are not properly declared with the keyword “var” are what are generally referred to as global leaks. Using strict mode will throw an exception in these instances.


### by reference or value?
In Javascripts, all arguments to a function are passed “by value” technically. That value, however, may be a reference to an object or the value of the variable. The simplest way to think about it that will generally work for you is to consider if the item is an object or primitive that you are passing in. A primitive, such as a string or integer, will be passed the actual value. A function or object will be passed the reference. Reassigning that variable does not change the referenced object, it simply assigns a new reference to the variable.


### closures
A closure is when a function closes around it’s current scope and that scope is passed along with the function object. This accomplished by returning an inner function. That inner function retains all scope it had including any variables that were declared in it’s parent function.


### Classes
There is no class keyword in Javascript. Instead, you simply defined a function normally would. To add methods to the class, you simply add them to the objects prototype.


### Inheritance
Javascript uses what it referred to as the prototype chain. Every object has a prototype, which will then have it’s own prototype property and so on. This will form a chain until the prototype property is null, which in most cases is on the Javascript Object prototype. When calling a methodor property on an object, Javascript first looks at all local properties for that object. If it doesn’t find it, it moves into the prototype. If it is still not found, it then moves into the next prototype and continues this process until the property or method is either found or prototype is null, at which point an exception will be thrown.


### anonomous functions
An anonomous function is simple any function that is not named. The common use for these are when passed as an argument into another function or any other time you don’t need to directly call that function directly from that same scope. Inside the function that it was passed into, the function isn’t actually anonomous anymore as it is given the variable name specified in the function declaration. One thing to consider is that when Javascript throws an error on an anonomous function, the output can be hard to follow. Simple adding a function name can make things considerable easier.


### async vs sync
In many languages, operations are all performed in a purely syncronous manner. The execution follows to code line by line waiting for each line to finish. In Javascript, you can also have asyncronous actions because of the way the event loop works. You’ve all seen this when passing in a function to a click handler in JQuery. The code doesn’t stop and wait for the click to happen before continuing, the JQuery click function sets up the proper events and return immediately. It has that callback function, though, that it can run whenever that event is triggered. One way to force an async function execution would be to add the code in a timeout or nextTick function. Those both say to wait an amount of time, which then allows the event loop to continue executing code.

In Node, async functions are particularly powerful as all IO runs through them, and IO is notoriously the largest blocker in most code, whether it’s reading from a database or opening a local file. This is an extremely important concept in Node’s speed. The ideal Node program is many small executions with async callbacks handling anything that takes any time. This way the program can continue processing instead of waiting around for the action to finish.

[http://howtonode.org/understanding-process-next-tick](http://howtonode.org/understanding-process-next-tick)


### callback pattern
As mentioned before, this is simply the design pattern of passing in a function to another function (usually as the last argument) with the intent of that function being called when the called function is finished with it’s task. Similar functionality can be handled with promises, and some people prefer to work with promises (they were a larger part of Node in early versions, but Node has transitioned completely to callback and event patterns).


### ECMAScript Latest
Node uses the latest build of V8 which has all of the newest features of ECMAScript 5.1 and even some limited features from ES6 when using the --harmony flag.

```node -e 'console.log(process.versions)'```


[http://v8.googlecode.com/svn/trunk/ChangeLog](http://v8.googlecode.com/svn/trunk/ChangeLog)
[http://addyosmani.com/blog/a-few-new-things-coming-to-javascript/](http://addyosmani.com/blog/a-few-new-things-coming-to-javascript/)
[http://dailyjs.com/2012/10/15/preparing-for-esnext/](http://dailyjs.com/2012/10/15/preparing-for-esnext/)


### native JSON
Node has JSON handling methods built in: stringify, parse. It can also load in a JSON file using the require() syntax. The file will be loaded as a Javascript object parsed from the JSON string.

### popular helper libraries
underscore is a great library for general Javascript use. async.js is a library specifically meant for handling asyncronous workflows. many