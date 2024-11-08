## open vs code create file name server
### open terminal :1. cd server   2.npm init -y, 3. npm install express cors mongoose jsonwebtoken bcryptjs cookie-parser dotenv morgan helmet

1. open package-json : "type" :"module",

## 2. type this index.js file:
{
 import express from 'express'
import cors from 'cors'
import dotenv from 'dotenv'
dotenv.config()
import cookieParser from 'cookie-parser'
import morgan from 'morgan'
import helmet from 'helmet'

const app  = express()
app.use(cors({
    credentials :true,
    origin:process.env.FRONTEND_URL
}))
app.use(express.json())
app.use(cookieParser())
app.use(morgan())
app.use(helmet({
    crossOriginResourcePolicy : false
}))

const PORT =8080 || process.env.PORT

app.listen(PORT,()=>{
    console.log(`Server is running`, PORT )
})




}
# run server :  node index.js
## 2.terminal : npm i nodemon

##### edit pacage-json file : "scripts": {
    "start" : "node index.js",
    "dev" :"nodemon index.js"

# final sever start : npm run dev

# open mongodb database create and connection 
## vs code config/ConnectDB.js
import mongoose from "mongoose";
import dotenv from 'dotenv'
dotenv.config()

if(!process.env.MONODB_URL){
  throw new Error(
    "please provide MONODB_URL in the .env file"
  )
}

async function ConnectDB() {
    try {
         await mongoose.connect(process.env.MONODB_URL)
         console.log("connect DB")
        
    } catch (error) {
        console.log("mongodb connection error", error)
        process.exit(1)
        
    }
    
}

export default ConnectDB;

### and create .env file 


 FRONTEND_URL=
 MONODB_URL = mongodb+srv://mdraihan51674:iVQJvw0qWqna0iXj@binkeyit.e3qis.mongodb.net/?retryWrites=true&w=majority&appName=Binkeyit

# Update index.js file 
import express from 'express'
import cors from 'cors'
import dotenv from 'dotenv'
dotenv.config()
import cookieParser from 'cookie-parser'
import morgan from 'morgan'
import helmet from 'helmet'
# import ConnectDB from './Config/ConnectDB.js'

const app  = express()
app.use(cors({
    credentials :true,
    origin:process.env.FRONTEND_URL
}))
app.use(express.json())
app.use(cookieParser())
app.use(morgan())
app.use(helmet({
    crossOriginResourcePolicy : false
}))

const PORT =8080 || process.env.PORT

app.get("/",(req, res)=>{
    //server to client
    res.json({
        message: "Server is running" + PORT
    })
})
#  ConnectDB()

app.listen(PORT,()=>{
    console.log(`Server is running`, PORT )
})












