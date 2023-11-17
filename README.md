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
      // result give an object which have a property containing
      // buffered data which needs to be converted in specific file.
      console.log(result.Body.toString('utf-8'))
    }
  }
)
```


<br>
<br>

# delete object from AWS S3 bucket
```javascript
const axios = require('axios');
const express = require('express');
const app = express();
const fs = require('fs');
const x = require("./func");
const AWS = require( 'aws-sdk' );

// const cloudFrontDistributionDomain = 'd19a566nyr3opx.cloudfront.net';
// const objectKey = 'image.jpg';



AWS.config.update({
  accessKeyId: 'AKIAUYPP6YV4XQS665GF',
  secretAccessKey: '9TND7wbQ8GCMeAFSOvPNrz0+k1gGdrZHJ2IHMizT',
  region: 'ap-south-1' ,// Change to your AWS region  

});


//initialize s3
// it must be after AWS.config
const s3 = new AWS.S3({apiVersion: 'latest'}); // s3 must initialize after AWS.config
const params = {
  Bucket : 'knigiimagedb',
  Key: 'nicetext.txt',
 
}


// confirm IAM user has AmazonS3FullAccess policy added
s3.deleteObject(params, (err, res) => {
  console.log(" \n beginning operation \n"); 
  // console.log(s3.config.credentials);
  if(err) {
    console.log(err);
  } 
  else {
    console.log("successful");
  }
})


```


<br>
<br>

# get Object using Axios from AWS cloudFront


```javascript
const axios = require('axios');

//error log: not uing "https://" in this cloudFrontDistributionDomain caused an error
// unable to get image since I didn't use "https://" in the variable
const cloudFrontDistributionDomain = 'https://d19a566nyr3opx.cloudfront.net';
const objectKey = 'image.jpg';
const apiUrl = cloudFrontDistributionDomain + "/" + objectKey;


axios.get(apiUrl)
  .then(function (response) {
    // Handle a successful response
    console.log('Response data:', response.data);
  })
  .catch(function (error) {
    // Handle any errors that occurred during the request
    console.error('Error:', error);
  });   
```

<br>
<br>

# Check if the data is binary(image data) or not 


```javascript
for (let i = 0; i < data.length; i++) {
      const charCode = data.charCodeAt(i);
      if (charCode < 32 || charCode > 127) {
        console.log("\n this data is binary \n");
        return true;
      }
    }
```

```javascript
axios.get(apiUrl)
  .then(function (response) {
    const data = response.data;
    // Handle a successful response
    // console.log('Response data:', response.data);
    // console.log(Buffer.isBuffer(response.data));
    for (let i = 0; i < data.length; i++) {
      const charCode = data.charCodeAt(i);
      if (charCode < 32 || charCode > 127) {
        console.log("\n this data is binary \n");
        return true;
      }
    }
  })
  .catch(function (error) {
    // Handle any errors that occurred during the request
    console.error('Error:', error);
  }); 
```


<br>
<br>

# slow process of reading image data from axios get reuqest and send it as response
```javascript
const fs = require('fs');

axios.get(apiUrl, { responseType: 'arraybuffer' })
  .then(function (response) {
    const binaryData = response.data;
    
    // Save the binary image data to a file (example: image.jpg)
    const imagePath = 'path_to_save_image.jpg'; // Replace with the desired file path
    fs.writeFileSync(imagePath, Buffer.from(binaryData), 'binary');
  })
  .catch(function (error) {
    console.error('Error:', error);
  });

```




<br>
<br>

# Read image data from AWS bucket using cloudFront and using AXIOS

```javascript
const axios = require('axios');
const express = require('express');
const app = express();

//error log: not uing https:// in this cloudFrontDistributionDomain caused an error
// unable to get image since I didn't use "https://" in the variable
const cloudFrontDistributionDomain = 'https://d19a566nyr3opx.cloudfront.net';
const objectKey = 'image.jpg';
const apiUrl = cloudFrontDistributionDomain + "/" + objectKey;

app.get('/' , ( req, res) => {
  res.send(`<img src="/image"/>`)
})


app.get('/image' , ( req, res ) => {
  axios.get(apiUrl, {responseType: 'arraybuffer'})
  .then(function (response) {

    res.send(response.data)

  })
  .catch(function (error) {
    // Handle any errors that occurred during the request
    console.error('Error:', error);
    
  });   


})

app.listen(8000);
```



# Structure of find() operation
* find() no longer supports callback.
* `find(criteria, condition, callback)`, it no longer supports the callback.
* It used callback to create asyncnonous function before.
* Now it is using promise to create asyncronous function.
* That's why it no longer supports callback.
* `find(criteria, condition)`.
* Now what could be behind the structure of the find()?



```javascript
class Mongoose {
    find(criteria, condition, otherArgument) {
        return new Promise( ( resolve, reject ) => {
            // produce promise depending on criteria
        } 
    }
}


// time to catch the promise using "async"
const b = async () => {
    try {
        let m =await ShopModel.find(
            {
                productTitle: "Woven Issue Four"
            }  
        )
        return m;
    }
    
    catch (error) {
        console.log(error);
    }
}

b()
.then( ( res ) => {
    console.log(res);
})
.catch( ( err ) => {
    console.log(err);
})

```

<br>
<br>

# Setting up route as module in different file(express.js)

```javascript
//MAIN FILE: index.js
const express = require( 'express' );
const mongoose = require ( 'mongoose' );
const app = express();



module.exports = app;
require('./src/routes/userRoutes');
```

```javascript
//ROUTE FILE: routeHandler.js
const app = require("../../index");

app.get("/", ( req,res ) => {
    res.send("this is index page")
})

app.listen(8000);
```

<br>
<br>
<br>

# reading image from client request and upload file to amazon aws s3 using mutler(expres middleware)

```javascript
app 
    .post('/api/v1/uploadImage', upload.single('test') ,async ( req, res ) => {
        try{
            let a = await req.file.filename;
        }

        catch (err ) {
            console.log(err)
        }
        
        console.log(req.file.filename); //returns object containing uploaded file
        // res.send(req.file);

        const x =fs.readFileSync(`${__dirname}/../../upload/${req.file.filename}`);
        s3.putObject({
            Body : x,
            Bucket : 'knigiimagedb',
            Key : `shopItem/${req.file.filename}.jpg`
        },
        ( err, data ) => {
            if(err) {
                console.log(err)
            }else {
                console.log("File Uploaded successful")
            }
        }
        ) // end of s3

        res.send("file uploaded")
    })

```




























