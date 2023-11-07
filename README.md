# Node.js-Code-library


# connecting to mongoDB and creating schema and inserting data into the database

```javascript
//install mongoose npm install mongoose
//require mongoose 
const mongoose = require ( "mongoose" );


// define url to connect to database
const url = "mongodb+srv://himahinulabid:DjYFI1UPxb5BRyJl@cluster0.kgeats8.mongodb.net/ManOfSteel?retryWrites=true&w=majority";
//ManOfSteel is the database name that I want to connect

// time to connect to mongodb

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



// SCHEMA/ PROTOTYPE FOR DOCUMENT
const X = new mongoose.Schema(
    {
        firstname: String, //always first character uppercase of type
        age: Number,  //always first character uppercase of type
        approve: Boolean  //always first character uppercase of type
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

<br>
<br>

# Mongoose model without Schema

```javascript
const User = mongoose.model('User', { 
    name:String , 
    age: Number  
}); 
```


<br>
<br>

# read mongoDB data find()

```javascript
const mongoose = require('mongoose');
const url = "mongodb+srv://himahinulabid:DjYFI1UPxb5BRyJl@cluster0.kgeats8.mongodb.net/ManOfSteel?retryWrites=true&w=majority";

const connectServer = () => {
    mongoose.connect(
            url, 
            {
                useNewUrlParser: true,
                useCreateIndex: true,
                useFindAndModify: false
            }
            
        ).then( ()=>{
            console.log("connection to database is successfull")
        });
}
connectServer(); 


const CatSchema = mongoose.Schema(
    {
        firstname: String,
        age: Number
    },
    {
        collection: "SupermanCollection"
    }
)


const CatModel = mongoose.model("SupermanCollection", CatSchema);

// find()

CatModel.find({firstname: "Clark Kent"}, (err, docs) =>{
    // the docs contains the result of the query of find function
    console.log(docs);
})
```

<br>
<br>

# Upload object in AWS S3 bucket

```javascript
//npm install aws-sdk
const AWS = require('aws-sdk');
const fs = require('fs');




// Set up AWS configuration
AWS.config.update({
  accessKeyId: 'AKIAUYPP6YV4XQS665GF',
  secretAccessKey: '9TND7wbQ8GCMeAFSOvPNrz0+k1gGdrZHJ2IHMizT',
  region: 'ap-south-1' // Change to your AWS region
});

// Initialize S3
const s3 = new AWS.S3();

s3.putObject(
  {
    Body: "hello worldsssss", // what the file should contain : a string 
    Bucket: 'knigiimagedb', //s3 bucket name
    Key: "myfile.txt" // specify the name of the file , the file will take place with this name in cloud
  },
  (err, data) => {
    if (err) {
      console.error("Error uploading file: ", err);
    } else {
      console.log("File uploaded successfully!");
    }
  }
);
```

<br>
<br>

# Read object from AWS S3 bucket

```javascript
//npm install aws-sdk
const AWS = require('aws-sdk');
const fs = require('fs');




// Set up AWS configuration
AWS.config.update({
  accessKeyId: 'AKIAUYPP6YV4XQS665GF',
  secretAccessKey: '9TND7wbQ8GCMeAFSOvPNrz0+k1gGdrZHJ2IHMizT',
  region: 'ap-south-1' // Change to your AWS region
});

// Initialize S3
const s3 = new AWS.S3();

s3.getObject(
  {
    Bucket: "knigiimagedb",
    Key: "myfile.txt"
  },
  ( err, result ) => {
    if( err ) {
      console.log( err );
    } else {
      console.log(result.Body.toString('utf-8'))
    }
  }
)
```
