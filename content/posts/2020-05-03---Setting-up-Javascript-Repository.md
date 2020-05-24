---
title: Algorithms in Javascript - Part 1
date: "2020-05-23"
template: "post"
draft: false
slug: "setting-javascript-repo"
category: "Algorithms"
tags:
  - "Anushree Bagchi"
  - "Javascript Repository"
description: "This article shows how to create a basic scaffolding for writing Javascript Programs"
socialImage: "/blog/media/photo.png"
---

I am going to start a series on how to write some of the popular algorithms and use datastructres in javascript. This series is going to be paricularly sueful for front developers who are preparing for DS & Algo for their interveiws.

Now the first step of our journey is to create a respository where we can start writing our algorithms. This seems to be a pretty straight forward problem but unfortunately its not. The problem is exacerbated by different versions of Javascript , Node js , etc. I was unable to find a good tutorial on how to setup a Node JS repo for writing programs in ES 6.

At the end of this article , we will 
1. A Node JS Git repo
2. We will be able to use the latest and greatest in EcmaScript.
3. We will not be tied to the latest Node Js versions.
4. We can easily debug using VS Code.

There are lot of blogs in the internet to assist while working on a JS project but none of them tells the detail on how to set up a new repository for a project. Hope this is helpful for people who have started there journey to learn Javascript.

Happy Learning :)

### Step 1: Creating a new repository in Git and push it ###

  * Create new folder. Open the folder in VS Code.
  * Initialize git - `git init`
  * Create new repository in GitHub.
  * Commit and push the new folder to Github.

### Step 2: Set up a new NodeJS repo that will create a new package.json file. ###
  
Navigate to root directory on command line and run the below command. 
```shell
npm init
```
Provide package name, version, description etc basic questionaire asked in command line and confirm. 
  
  ```
  name: (es6-demo) es6
  version: (1.0.0) 1.0.0
  description: ES6 demo
  entry point: (index.js)
  test command:
  git repository:
  keywords: es6
  author: Aushree
  license: (ISC)
  About to write to D:\projects\es6-demo\package.json:
  {
  "name": "es6",
  "version": "1.0.0",
  "description": "ES6 demo",
  "main": "index.js",
  "scripts": {
  "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [
  "es6"
  ],
  "author": "jstut",
  "license": "ISC"
  }
```

The above steps will create Package.json file which looks like

```json
{
  "name": "es6",
  "version": "1.0.0",
  "description": "ES6 demo",
  "main": "index.js",
  "scripts": {
  "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [
  "es6"
  ],
  "author": "jstut",
  "license": "ISC"
}
```

**Package.json** file holds various metadata relevant to the project. This file is used to give information to npm that allows it to identify the project as well as handle the project's dependencies. 
Read more about Package.json [here](https://docs.npmjs.com/creating-a-package-json-file)
  
**Creating code folder.**
  Create a src folder and add index.js file to the src folder. Add some code to the js files.

  ```
  console.log("Inside index.js");
  ```
  
**Executing the code in index.js file**

  Run below in command line to exceute the code in index.js. The logging should appear in the command line after the script is executed. 
  ```
  node src/index.js
  ```
We can install nodemon in our project folder. Nodemon is a utility that will monitor for any changes in our source and automatically restart our server. On executing the below on command line, will create a devDependencies section in package.json

  ```
  npm install nodemon --save-dev
  ```
  ```
  "devDependencies": {
    "nodemon": "^2.0.4"
  }
  ```

**Generating node_modules** 

The package. json file in the root defines all the libraries that will be installed into `node_modules` when you run npm install. Along with `node_modules` , Package-lock.json file also gets generated.

  ```
  npm install
  ```
**Package-lock.json**

Package-lock.json file holds the exact versioned dependency tree. This means you can guarantee the dependencies for other developers or prod releases.
You can read more about Package-lock.json [here](https://docs.npmjs.com/configuring-npm/package-locks.html) 


Next we can move the command to execute the index.js file in scripts section of our package.json.

  ```
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "nodemon src/index.js",
  }
  ```


  On the command line, run the script again, but this time with a npm start. Every time you change the underlying start script in the package.json file's npm scripts, you only need to type npm start on the command line without the specifics of the underlying script.

  Congratulations, we have set up our first JavaScript project with Node and npm.

  Now we will update our project folder a little bit. We will add one more file 'test.js' to src folder.
  We will add a logger to this file as well. And we will import this new file to our index.js 

  index.js will look like below:
  
  ```
  import "./test.js";
  console.log("Inside index.js");
  ```
  And the test.js file will look like this.

  ```
  console.log("Inside test.js");
  ```
  We will run the scripts again with npm start. This will immideately give below error.

  ```
  SyntaxError: Cannot use import statement outside a module
    at wrapSafe (internal/modules/cjs/loader.js:1047:16)
    at Module._compile (internal/modules/cjs/loader.js:1097:27)
    at Object.Module._extensions..js (internal/modules/cjs/loader.js:1153:10)
    at Module.load (internal/modules/cjs/loader.js:977:32)
    at Function.Module._load (internal/modules/cjs/loader.js:877:14)
    at Function.executeUserEntryPoint [as runMain] (internal/modules/run_main.js:74:12)
    at internal/main/run_main_module.js:18:47
  ```

  This is because we are using ES6, a new version of Javascript which is not supported. Inorder to use the ES6 we need to set up a transpiller which can convert ES6 code to ES5 which the browser can understand.


**Setting Up an ES6 Project Using Babel**

  **What is ES6** - This is a new version of Javascript which not all the vendor browsers support. 
  Therefore, if we want to use a new feature in ES6 and expect the old browsers to understand it, we must use a transpiler (Example - Babel).

  * Setting up ES6 transpiler Babel

  Run below command in command line. This will add babel libraries in devDependencies in package.json and will install in node_modules.

  ```
  npm install @babel/core @babel/node @babel/cli @babel/preset-env --save-dev; 
  ```

  ```
  "devDependencies": {
    "@babel/cli": "^7.8.4",
    "@babel/core": "^7.9.6",
    "@babel/preset-env": "^7.9.6",
    "@babel/node": "^7.8.7",
  }
  ```
  Update the start script in package.json.
  ```
  "scripts" : {
    "start": "nodemon --exec babel-node src/index.js"
  }
  ```

  Add .babelrc file

  ```
  {
    "presets": ["@babel/preset-env"],
    "env": {
      "debug": {
        "sourceMaps": "inline",
        "retainLines": true
      }
    }
  }
  ```

**Enabling debugger in VS code**

To enable the vscode debugging, add launch.json file in .vscode folder

```
{
    "version": "0.2.0",
    "configurations": [
		
        {
            "type": "node",
            "request": "launch",
            "name": "current file",
            "program": "${file}",
            "runtimeExecutable": "${workspaceRoot}/node_modules/.bin/babel-node",
            "sourceMaps": true,
            "env": {
              "BABEL_ENV": "debug"
            }
        },
		{
			"type": "node",
			"request": "attach",
			"name": "Attach",
			"restart": true,
			"port": 9229
		},
		{
			"type": "node",
			"request": "launch",
			"protocol": "inspector",
			"name": "ES6 Debugger",
			"program": "${workspaceFolder}/index.js",
			"runtimeExecutable": "${workspaceRoot}/node_modules/.bin/babel-node",
			"runtimeArgs": ["--presets", "env"]
		}
	]
}
```







