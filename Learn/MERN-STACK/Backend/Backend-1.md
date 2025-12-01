## Express.js (Backend Framework)

### Basic Server

- Install Express for the server
```bash
npm i express
```
- Install nodemon for dev usage
```bash
npm i nodemon
```

- In pac

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
const connectDB= require("./service/db.js")
dotenv.config();
const PORT =process.env.PORT;

connectDB();

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