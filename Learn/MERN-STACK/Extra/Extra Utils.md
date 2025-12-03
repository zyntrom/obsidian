## Setting up Dotenv (.env)

- Install dotenv
```bash
npm i dotenv
```

### index.js

```js
const dotenv= require("dotenv");
dotenv.config();
```

### Usage

```js
process.env.VARIABLE
```

## Setting up bcrypt

- Install bcrypt 
```bash
npm i bcrypt
```

- Usage of bcrypt

```js

const bcrypt = require("bcrypt);
const hashPassword= bcrypt.hash(password,10);
const isMatching= bcrypt.compare(password,hashPassword);

```

## Setting up JWT (jsonwebtoken)

- Install jwt (jsonwebtoken)
```bash
npm i
```