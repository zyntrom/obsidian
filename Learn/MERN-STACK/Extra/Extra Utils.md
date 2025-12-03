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
npm install jsonwebtoken
```
- Generate a jwt token
```js
const jwt =require("jsonwebtoken);

module.exports = (userId) =>{
	return jwt.sign(
		{
			id:useId
		},
		process.env.JWT_SECRET,
		{
			expireIn:"7d"
		}
	);
};
```

```.env
JWT_SECRET=secret_word
```
