# Mongoose Orm for Connecting MongoDb to Nodejs
Mongoose is an orm tool to easily connect mongodb with nodejs applications and provide methods to do various operations on the mongodb database.

# How to setup the mongoose on the nodejs or express app
## 1. Setup Steps:
1. Create a Nodejs project
2. Install Packages:
```
npm init -y
npm install express mongoose dotenv
npm install nodemon --save-dev
```
3. Create basic folders like:
- models/
- routes/
- controllers/
- config/
- app.js or server.js

4. Connect Mongodb using Mongoose
5. Create a Schema and Model
6. Create Routes for Crud.
7. Use express.json() to parse JSON body.
8. Run the server and test with Postman.

Mongoose models are created from schema, and Mongoose automatically maps model names to collection names in plural form.

## 2. Basic Project Structure:
```
project/
   models/
       user.model.js
   routes/
       user.routes.js
   controllers/
       user.controller.js
   .env
    server.js
```

## 3. Server Setup
```
//server.js
const express=require("express");
const mongoose=require("mongoose");
require("dotenv").config();

const app=express();
app.use(express.json());

mongoose.connect(process.env.MONGO_URI)
     .then(()=>console.log("Mongodb connected"))
     .catch((err)=>console.log(err));

app.get("/",(req,res)=>{
    res.send("API is running");
})

app.listen(5000, ()=>{
    console.log("Server running on port 5000");
});

```
## 4. Create Schema and Model
```
// models/user.model.js

const mongoose=require("mongoose");

const userSchema=new mongoose.Schema(
    {
        name: {type:String, required:true, trim:true},
        email: {type:String, required:true, unique:true },
        age: {type:Number, min:1},
        isActive: {type: Boolean, default:true}
    },
    {timestamps:true}
);

const User= mongoose.model("User",userSchema);

module.exports=User;

```

A schema defines the structure and rules of a document, and a model is what you use to query and modify the database.

## 5. Crud Operations
### Create
```
const User=require("../models/user.model");

const createUser=async (req,res)=>{
    try{
        const user=await User.create(req.body);
        res.status(201).json(user);
    }
    catch(error){
        res.status(500).json({
            message:error.message
        })
    }
};
```

### Read All
```
const getUser=async (req,res)=>{
    try{
        const users=await User.find();
        res.json(users);
    }
    catch(error){
        res.status(500).json({
            message:error.message
        })
    }
};
```

### Read One
```
const getUserById=async (req,res)=>{
    try{
        const user=await User.findById(req.params.id);

        if(!user) return res.status(404).json({message:"User Not Found"});

        res.json(user);
    }
    catch(error){
        res.status(500).json({
            message:error.message
        })
    }
};
```

### Update
```
const updateUser=async (req,res)=>{
    try{
        const user=await User.findByIdAndUpdate(
            req.params.id,
            req.body,
            {new:true, runValidators:true}
        );

        if(!user)  return res.status(404).json({message:"User Not Found"});

        res.json(user);
    }
    catch(error){
        res.status(500).json({message:error.message});
    }
};
```

### Delete
```
const deleteUser= async (req,res)=>{
    try{
        const user=await User.findByIdAndDelete(req.params.id);

        if(!user) return res.status(404).json({message:"User not Found!});

        res.json({message:"User deleted Successfully.});
    }
    catch(error){
        res.status(500).json({message:error.message});
    }
}
```

Mongoose supports common model methods like create, find, findById, findByIdAndUpdate, findByIdAndDelete, deleteOne, deleteMany and aggregate.

## 6. Routes

```
//   routes/user.routes.js
const express=require("express");
const router=express.Router();

const {
    createUser,
    getUsers,
    getUserByid,
    updateUser,
    deleteUser
    }= require("../controllers/user.controller");


    router.post("/",createUser);
    router.get("/",getUsers);
    router.get("/:id",getUserById);
    router.put("/:id",updateUser);
    router.delete("/:id",deleteUser);\

    module.exports=router;
```

Then use it in server:
```
const userRoutes=require("./routes/user.routes");
app.use("/api/users",userRoutes);
```

## 7. Important Mongoose Methods
#### Model Methods:
These are methods you use on the model itself, like User.find() or User.create().

- create(): inserts a new document.
- find(): gets all matching documents.
- findOne(): gets first matching document.
- findById(): gets document by _id.
- insertMany(): inserts multiple documents.
- updateOne(): updates One Matching document.
- updateMany(): updates many document
- deleteOne(): deletes one matching document
- deleteMany(): deletes many documents.
- findByIdAndUpdate(): finds by Id and update
- findOneAndUpdate()
- findByIdAndDelete(): finds by id and deletes.
- findOneAndDelete()
- countDocuments(): count matching docs.
- exists(): check if the result exists
- aggregate(): performs aggregation pipeline

Example:
```
const users=await User.find();
const user=await User.create({name:"Anshuman", email:"a@test.com"});
```

#### Document Methods:
These are the methods you use on a single document object returned from the database.

- save(): saves a document instance.
- validate(): validates before saving.
- toObject(): convert from json to javascript object
- toJSON(): convert simple js object to json
- deleteOne()
- isModified()
- markModified()
- increment()

Example:
```
const user=await User.findById(id);
user.name="New Name";
await user.save();
```

#### Query Methods:
- sort(): sorts results.
- limit(): limits results.
- skip(): skips records for pagination
- select(): selects specific fields
- populate(): joins referenced documents.

# Explaination of Different Types Of Mongoose methods:
Mongoose Methods are divided into four types:
1. Model methods: Mongoose model methods are used directly on the model for database operations like find, create, and update.
2. Document method: Document methods works on a single returned record, like save() or validate().
3. Instance Method: Instance methods are custom methods defined on `schema.methods` for per-document behaviour.
4. Static method: Static Methods are defined on schema.statics for model-level reusable logic.

## Common Model Methods Explaination:
These are used on the Model itself, like `User.find()` or `User.create()`.

#### create()
Creates and saves a document in one step.
```
const user=await User.create({name:"Anshuman", email:"a@test.com"});
```
#### find()
Finds all matching documents.
```
const users=await User.find({});
```

#### findOne()
FInds the first matching document.
```
const user=await User.findOne({email:"a@test.com"});
```

#### findById()
Finds a document by _id
```
const user=await User.findById(id);
```

#### updateOne()
Updates the first matching document.
```
await User.updateOne({email:"a@test.com"},{$set:{name:"New Name"}})
```

#### updateMany()
Updates all matching documents.
```
await User.updateMany({isActive:false},{$set:{isActive:true}});
```

#### findByIdAndUpdate()
Finds one document and update it.
```
const user=await User.findByIdAndUpdate(
    id,
    {name:"Updated Name"},
    {new:true,runValidators:true}
)
```

#### findOneAndUpdate()
Finds One Document and updates it.

```
const user=await User. findOneAndUpdate({
    {email:"a@test.com"},
    {name:"Updated Name"},
    { new:true}
})
```
