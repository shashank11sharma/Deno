# Deno
What is Deno.js?
 
A secure runtime for JavaScript and TypeScript.
 
The makers of the widely used JavaScript server-side runtime, Node.js, have released Deno 1.0, a new runtime for JavaScript and TypeScript that addresses "design mistakes" in Node.js.
 
The Deno JavaScript project has been under development by Node.js creator Ryan Dahl for the past two years and his team of contributors has now released Deno 1.0, which could become just as important for JavaScript developers as Node.js.
 
What’s wrong with Node.js?
 
The most important thing first: Nothing is wrong with Node.js. You can use it and you should not switch to Deno just because it’s there.
 
Node.js is getting used by thousands of (very large) companies, it has huge ecosystem and a highly active community - Node.js isn’t going anywhere!
 
You don’t have to take this from me by the way - you can also listen to Ryan.
 
But there are a couple of weaknesses in Node.js which could potentially be improved (side-note: Those weaknesses of course don’t necessarily have to matter to you).
Node.js is focused on JavaScript and doesn’t (natively) use static types
The import syntax is very specific to Node.js and not what we know from the browser (ES modules, URL imports)
Node.js does not embrace modern JavaScript features like Promises
Node.js is not "secure by default"
The last point is a tricky one though. “not secury by default” sounds horrible and it’s easy to get this point wrong.
 
Node.js absolutely allows you to build secure applications. Period!
 
BUT
A Node script doesn’t have a built-in security model. To be precise, by default, every Node script has full access to your file system, your network and your entire environment.
 
This is by design and makes Node.js very flexible. But it also means that tools like ESLint, which are just “big Node.js scripts” under the hood, theoretically could do anything with your files on your system.
 
How does Deno fix those problems?
 
Deno generally can be used for the same things as Node.js. You can use it to build web servers, you can use it to build utility scripts etc.
 
But Deno,
By default supports TypeScript - hence it’s a JavaScript and TypeScript runtime
Uses ES modules (with URL support) imports instead of its own module system
Embraces modern JavaScript features like Promises or async iterables
Is “secure by default”
Let’s take a closer look at those points then.
 
TypeScript Support
 
You can absolutely write normal JavaScript code with Deno - but if you want, you can also switch to TypeScript at any point as the TypeScript compiler is built right into Deno.
 
For example, this code would fail when executed with Node.js but works with Deno,
let message: string // TypeScript feature!  
message = 'Hi'  
console.log(message)   
The usage of TypeScript of course gives you extra type safety and might help you avoid a lot of unnecessary bugs.
 
As mentioned, it’s optional but if you want to use it, you don’t have to set up your own custom TypeScript project and compilation flow first.
 
ES Modules Imports
 
Node.js brings its own modules system,
const http = require('http')  
const somethingFromMyFile = require('./my-file')   
We got used to it but it’s very different from what we know in the browser,
import something from './someFile.js'  
import { someFunction } from 'https://cdn.some-page.com/some-package.js' // yes, this works!   
or - directly in HTML of course,
<script src="https://cdn.some-page.com/some-package.js"></script>   
In the browser, we use relative or absolute URLs. We don’t sometimes use module names and sometimes file paths (both is done in Node).
 
In addition, in Node projects, we use npm to manage our local packages. This tool downloads them and stores them (as well as their dependencies) in the node_modules folder.
 
This folder can easily become very big and it’s actually an important part of Node’s module resolution system. Indeed, the following code relies on express existing as a package in node_modules - it would fail if it would be a simple express.js file or anything like that.
const express = require('express')   
Deno simplifies this. You simply work with ES Module imports (i.e. the syntax you know from browser-side JavaScript) and it doesn’t need a package managing tool or folder like npm/node_modules.
 
Instead, your Deno code looks like this,
import { serve } from 'https://deno.land/std@0.50.0/http/server.ts'   
This imports the serve function from the server.ts package which is stored on some web server.
 
Deno automatically downloads and caches this package (and its dependencies) when your code runs for the first time.
 
Modern JavaScript Features
 
Node.js works a lot with callback functions - simply because at the point of time it was created, modern JS functionalities like Promises weren’t as important and big (and common) as they are today.
 
Deno, being very new, of course is able to work around that and leverage all those modern features.
 
Hence you can for example spin up a very simple web server with the following code snippet that leverages “async iterables” (what is that?).
import { serve } from 'https://deno.land/std@0.50.0/http/server.ts'  
const server = serve({ port: 3000 })  
for await (const req of server) {  
   req.respond({ body: 'Message from Deno!' })  
}   
Just as a comparison, here’s pretty much the same server, built with Node.js,
const http = require('http');  
const server = http.createServer((res, res) => {  
   res.end('Message from Node');  
});  
server.listen(3000);   
Security
 
As mentioned, Deno has “security built in”.
 
And this does not mean that your Deno applications are always secure, no matter what you do!
 
This just means that Deno scripts can’t do everything on your computer by default.
 
For example, if you run the above server script, you’ll get an error message,
 
deno run my-server.ts
 
The script only executes successfuly once you use the right permissions,
 
deno run --allow-net my-server.ts
 
In this case, --allow-net provides network access to the script. Similar permission flags exist for writing (--allow-write) and reading (--allow-read) files for example.
 
Deno is extremely new. Version 1.0 was released on May 13th 2020. And just because it’s v1.0 does not mean that it’s finished and you should use it for your production apps.
 
It’s still very new and under active development. And it’s also way too early to tell whether it’ll ever be a “big thing”.
 
You can of course play around with it, dive into it and its ecosystem of packages and use it in your side projects or in demos and smaller apps.
 
But only time will tell if it’ll be adopted by bigger companies and projects and if the problems, which it fixes, are really problems with Node.js for the majority of other developers as well.
 
references
https://deno.land/
https://deno.land/v1

