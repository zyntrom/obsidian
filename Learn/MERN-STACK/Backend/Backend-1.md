## Express.js (Backend Framework)

- Install Express for the server
```bash
npm i express
```
- Install nodemon for dev usage
```bash
npm i nodemon
```

- In package.json add:
```json
//in script session add
"start":"node src/index.js",
"dev":"nodemon src/index.js"
```

### Basic Server

```js
const express =require("express");
const PORT =5000;
const app =express();

app.use(express.json());

app.get("/",(req,res)=>{
	res.json({"message":"Hello"});
})

app.listen(PORT,()=>{
	console.log("Server Running at port: "+PORT+" http://localhost:"+PORT);
})
```

## Basic Folder Structure

```bash
backend/
│── src/
│   │── index.js              # Entry point              
│   │
│   ├── service/
│   │   └── db.js             # Database connection
│   │
│   ├── controllers/          # All controller functions
│   │   └── userController.js
│   │
│   ├── models/               # Mongoose schemas/models
│   │   └── User.js
│   │
│   ├── routes/               # Express routes
│   │   └── userRoutes.js
│   │
│   ├── middleware/           # Middleware (auth, error handler, etc.)
│   │   ├── auth.js
│   │   └── errorHandler.js
│   │
│   ├── utils/                # Helper functions (JWT, email, etc.)
│   │
├── .env                      # Environment variables
├── package.json
└── README.md

```


## Basic Code Flow
### index.js

```js
const express =require("express");
const PORT =5000;
const app =express();
const homeRouter= require("./routes/homeRouter.js");
app.use(express.json());

app.use("/home",homeRouter);

app.listen(PORT,()=>{
	console.log("Server Running at port: "+PORT+" http://localhost:"+PORT);
})
```

### router/homeRouter.js

```js
const express = require("express")
const router = express.Router();

const {getHome}= require("../controllers/homeController.js");

router.get("/",getHome);

module.exports =router;
```

### controller/homeController.js

```js
 exports.getHome= (req,res)=>{
	 res.json({"message":"hello"});
 };
```

## Database Connection (MongoDB)

- Install mongoose 

```bash
npm i mongoose
```
### service/db.js

```js
const mongoose= require("mongoose");

const connectDB =async ()=>{
	try{
		const conn= await mongoose.connect(process.env.MONGO_URL);
		console.log("MongoDB Connected");
	}catch(err){
		console.log(err);
	}
}

module.exports =connectDB;
```

### index.js

```js
const express =require("express");
const dotenv= require("dotenv");

dotenv.config();
const PORT =process.env.PORT;

//DATABASE Connection
const connectDB= require("./service/db.js")
connectDB();
//DATABASE Connection

const app =express();
const homeRouter= require("./routes/homeRouter.js");
app.use(express.json());

app.use("/home",homeRouter);

app.use((err,req,res,next)=>{
	console.log(err);

	res.status(err.status || 500).json({
		"message":err.message || "Server Error"
	})
})
app.listen(PORT,()=>{
	console.log("Server Running at port: "+PORT+" http://localhost:"+PORT);
```

### Error Handling 

```js
app.use((err,req,res,next)=>{
	console.log(err);
	res.status(err.status || 500).json({
		"message":err.message || "Server Error"
	})
})
```
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

## Mongoose and DB models

