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

### Creating Models (User.js)

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

### CRUD controller Operations (userController.js)

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

### Router for the DB controllers (userRouter.js)

```js
const express= require("express");
const userController= require("../controllers/userController.js");

const router= express.Router();

router.post("/user/create",userController.createUser);
router.get("/user/",userController.getUsers);
router.get("/user/:id",userController.getUserById);
router.put("/user/:id",userController.updateUserById);
router.delete("/user/:d",userController.deleteById);

module.exports= router; 
```

### index.js

```js
const userRouter= require("./routes/userRouter.js");
app.use("/api/auth",userRouter);
```
