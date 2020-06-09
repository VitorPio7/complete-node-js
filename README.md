# The Complete Guide to Advanced React Component Patterns

## Table of Contents

- [The Complete Guide to Advanced React Component Patterns](#the-complete-guide-to-advanced-react-component-patterns)
  - [Table of Contents](#table-of-contents)
  - [**Section 1: Welcome**](#section-1-welcome)
  - [**Section 2: Installing and Exploring Node.js**](#section-2-installing-and-exploring-nodejs)
  - [**Section 3: Node.js Module System (Notes App)**](#section-3-nodejs-module-system-notes-app)
    - [Importing Node.js Core Modules](#importing-nodejs-core-modules)
    - [Importing Your Own Files](#importing-your-own-files)
    - [Importing npm Modules](#importing-npm-modules)
    - [Printing in Color](#printing-in-color)
    - [Global npm Modules and nodemon](#global-npm-modules-and-nodemon)
  - [**Section 4: File System and Command Line Args (Notes App)**](#section-4-file-system-and-command-line-args-notes-app)
    - [Getting Input from Users](#getting-input-from-users)
    - [Argument Parsing with Yargs](#argument-parsing-with-yargs)
    - [Storing Data with JSON](#storing-data-with-json)
  - [**Section 5: Debugging Node.js (Notes Apps)**](#section-5-debugging-nodejs-notes-apps)
  - [**Section 6: Asynchronous Node.js (Weather App)**](#section-6-asynchronous-nodejs-weather-app)
  - [**Section 7: Web Servers (Weather App)**](#section-7-web-servers-weather-app)
  - [**Section 8: Accessing API from Browser (Weather App)**](#section-8-accessing-api-from-browser-weather-app)
  - [**Section 9: Application Deployment (Weather App)**](#section-9-application-deployment-weather-app)
  - [**Section 10: MongoDB and Promises (Task App)**](#section-10-mongodb-and-promises-task-app)
  - [**Section 11: REST APIs and Mongoose (Task App)**](#section-11-rest-apis-and-mongoose-task-app)
  - [**Section 12: API Authentication and Security (Task App)**](#section-12-api-authentication-and-security-task-app)
  - [**Section 13: Sorting, Pagination, and Filtering (Task App)**](#section-13-sorting-pagination-and-filtering-task-app)
  - [**Section 14: File Uploads (Task App)**](#section-14-file-uploads-task-app)
  - [**Section 15: Sending Emails (Task App)**](#section-15-sending-emails-task-app)
  - [**Section 16: Testing Node.js (Task App)**](#section-16-testing-nodejs-task-app)
  - [**Section 17: Real-Time Web Applications with Socket.io (Chat App)**](#section-17-real-time-web-applications-with-socketio-chat-app)
  - [**Section 18: Wrapping Up**](#section-18-wrapping-up)

## **Section 1: Welcome**

- [Complete NodeJS](complete-node-js.pdf)
- [Source Code](https://github.com/andrewjmead/node-course-v3-code)

**[⬆ back to top](#table-of-contents)**

## **Section 2: Installing and Exploring Node.js**

**[⬆ back to top](#table-of-contents)**

## **Section 3: Node.js Module System (Notes App)**

### Importing Node.js Core Modules

```javascript
const fs = require('fs')

fs.writeFileSync('notes.txt', 'My name is Chester.')
fs.appendFileSync('notes.txt', ' I live in Singapore.')
```

```console
node app.js
```

**[⬆ back to top](#table-of-contents)**

### Importing Your Own Files

[Introduction to CommonJS](https://flaviocopes.com/commonjs/)

```javascript
const getNotes = () => 'Your notes...'

module.exports = getNotes 
```

```javascript
const getNotes = require('./notes.js')
const msg = getNotes()
```

**[⬆ back to top](#table-of-contents)**

### Importing npm Modules

```console
npm init -y
npm i validator
```

```javascript
const validator = require('validator')
console.log(validator.isURL('https://mead.io/')) 
```

**[⬆ back to top](#table-of-contents)**

### Printing in Color

```console
npm i chalk
```

```javascript
const chalk = require('chalk')
const greenMsg = chalk.green.inverse.bold('Success!')
```

**[⬆ back to top](#table-of-contents)**

### Global npm Modules and nodemon

```console
npm i -g nodemon
nodemon app.js
```

**[⬆ back to top](#table-of-contents)**

## **Section 4: File System and Command Line Args (Notes App)**

### Getting Input from Users

```javascript
const command = process.argv[2]

if (command === 'add') {
  console.log('Adding note!')
} else if (command === 'remove') {
  console.log('Removing note!')
}
```

```console
node app.js add
```

**[⬆ back to top](#table-of-contents)**

### Argument Parsing with Yargs

```javascript
const yargs = require('yargs')

// Create add command
yargs.command({
  command: 'add',
  describe: 'Add a new note',
  builder: {
    title: {
      describe: 'Note title',
      demandOption: true,
      type: 'string'
    },
    body: {
      describe: 'Note body',
      demandOption: true,
      type: 'string'
    }
  },
  handler: function (argv) {
    console.log('Title: ' + argv.title)
    console.log('Body: ' + argv.body)
  }
})

// Create remove command
yargs.command({
  command: 'remove',
  describe: 'Remove a note',
  handler: function () {
      console.log('Removing the note')
  }
})

// Create list command
yargs.command({
  command: 'list',
  describe: 'List your notes',
  handler: function () {
      console.log('Listing out all notes')
  }
})

// Create read command
yargs.command({
  command: 'read',
  describe: 'Read a note',
  handler: function () {
      console.log('Reading a note')
  }
})

module.exports = yargs 
```

```javascript
const yargs = require('./yargs')
console.log(yargs.argv)
yargs.parse()
```

```console
node app.js add
node app.js remove
node app.js list
node app.js read
node app.js add --title="My Note" --body="Interesting Lesson"
```

**[⬆ back to top](#table-of-contents)**

### Storing Data with JSON

```javascript
const book = {
  title: 'Ego is the Enemy',
  author: 'Ryan Holiday'
}

const bookJSON = JSON.stringify(book)
const parseData = JSON.parse(bookJSON)
```

```json
{
  "title": "Ego is the Enemy",
  "author": "Ryan Holiday"
}
```

```javascript
// const dataBuffer = fs.readFileSync('1-json.json')
// const dataJSON = dataBuffer.toString()
// const user = JSON.parse(dataJSON)

const user = require('./1-json.json')
user.name = 'Gunther'
user.age = 54

const userJSON = JSON.stringify(user, false, 2)
fs.writeFileSync('1-json.json', userJSON)
```

```json
{
  "title": "Ego is the Enemy",
  "author": "Ryan Holiday",
  "name": "Gunther",
  "age": 54
}
```

## **Section 5: Debugging Node.js (Notes Apps)**

**[⬆ back to top](#table-of-contents)**

## **Section 6: Asynchronous Node.js (Weather App)**

**[⬆ back to top](#table-of-contents)**

## **Section 7: Web Servers (Weather App)**

**[⬆ back to top](#table-of-contents)**

## **Section 8: Accessing API from Browser (Weather App)**

**[⬆ back to top](#table-of-contents)**

## **Section 9: Application Deployment (Weather App)**

**[⬆ back to top](#table-of-contents)**

## **Section 10: MongoDB and Promises (Task App)**

**[⬆ back to top](#table-of-contents)**

## **Section 11: REST APIs and Mongoose (Task App)**

**[⬆ back to top](#table-of-contents)**

## **Section 12: API Authentication and Security (Task App)**

**[⬆ back to top](#table-of-contents)**

## **Section 13: Sorting, Pagination, and Filtering (Task App)**

**[⬆ back to top](#table-of-contents)**

## **Section 14: File Uploads (Task App)**

**[⬆ back to top](#table-of-contents)**

## **Section 15: Sending Emails (Task App)**

**[⬆ back to top](#table-of-contents)**

## **Section 16: Testing Node.js (Task App)**

**[⬆ back to top](#table-of-contents)**

## **Section 17: Real-Time Web Applications with Socket.io (Chat App)**

**[⬆ back to top](#table-of-contents)**

## **Section 18: Wrapping Up**

**[⬆ back to top](#table-of-contents)**
