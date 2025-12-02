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

