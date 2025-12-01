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

## Mongoose and DB models

- Install Mongoose
```bash
npm i mongoose
```

### Creating Models

```js
const mongoose = require("mongoose");

const userSchema= new mongoose.Schema({
	name:{
		type:String,
		required:true
	},
	email:{
		type:String,
		required:true
	},
	password:{
		type:String,
		required:true
	}

},{timestamps:true});

module.exports= mongoose.model("User",userSchema);
```

### CRUD controller Operations

```js
const User= require("../models/User.js")

//Creating a user (inserting into the db)

exports.createUser= async (req,res,next)=>{
	try{
		const user = await User.create(req.body);
		res.status(201).json({
			success:true,
			user
		})
	}catch(err){
		next(err);
		console.log(err);
	}
}
//Getting all users (Getting all the data stored in the collection)

exports.getUsers=async (req,res,next)=>{
	try{
		const users= await User.find();
		res.json({
			success:true,
			users
		})
	}catch(err){
		next(err)
	}
}

//Getting a specific collection

exports.getUserById= async (req,res,next)=>{
	try{
		const user= await User.findById(req.params.id);
		res.json({
			success:true,
			user
		})
	}
	catch(err){
		next(err);
	}
}
//Updating an existing collection

exports.updateUserById = async (req,res,next)=>{
	try{
		const user= await User.findByIdAndUpdate(
			req.params.id,
			req.body,
			{new:true}
		);
		res.json({
			success:true,
			user
		})
	}catch(err){
		next(err);
	}
}
//deleting an existing collection

exports.deleteById= async (req,res,next)=>{
	try{
		await User.findByIdAndDelete(req.params.id);
		res.json({
			message:"User Deleted"
		})
	}
	catch(err){
		next(err);
	}
}
```

### Rou
