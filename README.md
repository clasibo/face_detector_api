Thw server made with node.js,  expres.js framewor and npm packages: cors and knex. <br><br>


const express = require('express');<br>
const bodyParser = require('body-parser');<br>
const bcrypt = require('bcrypt-nodejs');<br>
const cors = require('cors');<br>
const knex = require('knex');<br>
const register = require('./controllers/register');<br>
const signin = require('./controllers/signin');<br>
const profile = require('./controllers/profile');<br>
const image = require('./controllers/image');<br>

const app = express();<br><br>

app.use(bodyParser.json());<br>
app.use(cors());vv

const db = knex({<br>
    client: 'pg',<br>
    connection: {<br>
      host : '127.0.0.1',<br>
      port : 5432,<br>
      user : 'postgres',<br>
      password : 'test',<br>
      database : 'face_detector_db'<br>
    }  <br>
  });<br><br>
  app.get('/', (req, res) => {<br>
    res.send(db.users)<br>
})<br><br>

app.post('/signin', (req, res) => {signin.handleSignin (req, res, bcrypt, db)})<br>
app.post('/register', (req, res) => {register.handleRegister (req, res, bcrypt, db)})<br>
app.get('/profile/:id', (req, res) => {profile.handleProfileGet(req, res, db)})<br><br>

app.put('/image', (req, res) => {image.handleImage(req, res, db)})<br>
app.listen(process.env.PORT || 2000, () => {<br>
    console.log(`success .. the app is running on ${process.env.PORT}`)<br>
})<br>