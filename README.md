# Node.js-Code-library


### connecting to mongoDB and creating schema and inserting data into the database

```javascript
//install mongoose npm install mongoose
//require mongoose 
const mongoose = require ( "mongoose" );
const express = require("express");
const app = express();

// define url to connect to database
const url = "mongodb+srv://himahinulabid:DjYFI1UPxb5BRyJl@cluster0.kgeats8.mongodb.net/ManOfSteel?retryWrites=true&w=majority";

// time to connect to mongodb
const ConnectServer = () => {
    mongoose.connect(
        url,
        {
            useNewUrlParser:true,
            useCreateIndex: true,
            useFindAndModify:false
        }
    ).then((con) => {
        console.log(`
        
    >>>>> data connection successful!!!!!`);
    
    });

}
ConnectServer();

// SCHEMA/ PROTOTYPE FOR DOCUMENT
const X = new mongoose.Schema(
    {
        firstname: String,
        age: Number,
        approve: Boolean
    },

    {
        collection: "SupermanCollection"
    }
)


const Z = mongoose.model("Hello", X);

const testInsert = new Z({
    firstname: "Hello I set up another data data",
    age: 28,
    approve: true,
    moredata: "someting",
    anotherData : "some more data"
})


testInsert.save().then(()=>{
    console.log("successfully inserted into database");
})




// STEP BRIEF
// install and require mongoose 
// get url to connect to mongodb cluster 
// connect to mongodb using mongoose







```
