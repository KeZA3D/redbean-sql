# RedBeanNode

**(Early Development)**

RedBeanNode is an easy to use **ORM** tool for Node.js, strongly inspired by RedBeanPHP.
!!!WARNING!!! redbean-sql is last (0.0.20) version of `redbean-node` with bug fixes

Original:
https://www.npmjs.com/package/redbean-node

- **Automatically** creates **tables** and **columns** as you go
- No configuration, just fire and forget
- Ported RedBeanPHP's main features and api design
- Build on top of knex.js
- Supports **JavaScript** & **TypeScript**
- **async/await** or **promise** friendly

## Supported Databases

- MySQL / MariaDB
- SQLite

## Installation

```shell script
npm install redbean-node --save
```

## Code Example

This is how you do CRUD in RedBeanNode:

```javascript
const { R } = require("redbean-node");

// Setup connection
R.setup();

(async () => {
  let post = R.dispense("post");
  post.text = "Hello World";

  // create or update
  let id = await R.store(post);

  // retrieve
  post = await R.load("post", id);

  console.log(post);

  // delete
  await R.trash(post);

  // close connection
  await R.close();
})();
```
This **automatically generates** the tables and columns... on-the-fly. It infers relations based on naming conventions.

## New

Added `getSlots(array)`

```javascript
/**
* @param {Array} array
*/
genSlots(array = []) {
    if (!Array.isArray(array)) return undefined
    var str = array.slice();
    str.length ? str.fill("?").join() : ''
    return str
}
```

## Fixed

Fixed relations

```javascript
let car = db.R.dispense('car');
    car.brand = 'Brand';
    car.model = 'Model';
    car.year = 'Model';
    car.chat_keyword= 'KWD';
    try {await db.R.store(car);}catch (e) {console.log(e);}

    console.log("Creating usercar model");
    let usercar = db.R.dispense('usercar');
    usercar.added_date = db.R.isoDate();
    usercar.car = car; // Now this store correctly without any errors
    try {await db.R.store(usercar);}catch (e) {console.log(e);}
```