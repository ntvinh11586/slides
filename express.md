
class: center, middle

# Express

Building your first node.js server.

---

# Why not use `http`?

- Very low level
- No cookie handling or parsing
- No session support
- No routing
- No static file serving

---

# `http`: Example

```javascript
let http = require('http')


  






.
```

---

# `http`: Example

```javascript
let http = require('http')

let server = http.createServer((req, res) => {
  




})

server.listen(8000, '127.0.0.1')
```

---

# `http`: Example

```javascript
let http = require('http')

let server = http.createServer((req, res) => {
  res.writeHead(200, {'Content-Type': 'application/json'})
  let result = { version: '1.0.0' }
  res.end(JSON.stringify(result))


})

server.listen(8000, '127.0.0.1')
```

---

# `http`: Example

```javascript
let http = require('http')

let server = http.createServer((req, res) => {
  switch(req.url) {
    case '/version': version(req, res); break;
    case '/user': user(req, res); break;
    default: notFound(req, res); break;
  }
})

server.listen(8000, '127.0.0.1')
```

---

# `http`: Example

```javascript
let http = require('http')


//switch(req.url) {
//  case '/version': version(req, res); break;
//  case '/user': user(req, res); break;
//  default: notFound(req, res); break;



server.listen(8000, '127.0.0.1')
```

---

# `http`: Example

```javascript
let express = require('express')
let app = express()

//switch(req.url) {
//  case '/version': version(req, res); break;
//  case '/user': user(req, res); break;
//  default: notFound(req, res); break;



server.listen(8000, '127.0.0.1')
```

---

# Express: Example

```javascript
let express = require('express')
let app = express()

//switch(req.url) {
    app.get('/version', version)
//  case '/user': user(req, res); break;
//  default: notFound(req, res); break;



server.listen(8000, '127.0.0.1')
```

---

# Express: Example

```javascript
let express = require('express')
let app = express()

//switch(req.url) {
    app.get('/version', version)
    app.get('/user', user)
//  default: notFound(req, res); break;



server.listen(8000, '127.0.0.1')
```

---

# Express: Example

```javascript
let express = require('express')
let app = express()

//switch(req.url) {
    app.get('/version', version)
    app.get('/user', user)
    app.all(notFound)



server.listen(8000, '127.0.0.1')
```

---

# Express: Example

```javascript
let express = require('express')
let app = express()


app.get('/version', version)
app.get('/user', user)
app.all(notFound)



server.listen(8000, '127.0.0.1')
```

---


# Express

### Why use a framework?
- Foundation for iteroperability & code reuse
- Battle tested: memory leaks, bugs, stability, debugging

### Why use Express?
- Simple REST API routing
- Massive middleware ecosystem ("There's a middleware for that")
- Over 50% market-share

---

# Middleware

A function passed to `app.use()` or a route that accepts `(req, res, next) => {}`:

```javascript
app.use((req, res, next) => {
  // Terminate the response with .end() or .send()
  // Or mutate the response and call next()
})
```

---

# Middleware: Examples

**Middleware are opt-in. Include what you want:**
- Static files: `express.static()`
- Logging: `morgan`
- Body parsing: `body-parser`
- Cookie parsing: `cookie-parser`
- Session handling: `express-session`
- Authentiction: `passport`
- etc...

---

# Middleware: Stack

**Middleware are ordered like an array:**

```javascript
let app = express()










app.listen(8080, '127.0.0.1')
```

---

# Middleware: Stack

**Middleware are ordered like an array:**

```javascript
let app = express()

// Log every request to the console
app.use(morgan('dev')) 







app.listen(8080, '127.0.0.1')
```

---

# Middleware: Stack

**Middleware are ordered like an array:**

```javascript
let app = express()

// Log every request to the console
app.use(morgan('dev')) 

// Read and parse cookies
app.use(cookieParser('ilovethenodejs'))




app.listen(8080, '127.0.0.1')
```

---

# Middleware: Stack

**Middleware are ordered like an array:**

```javascript
let app = express()

// Log every request to the console
app.use(morgan('dev')) 

// Read and parse cookies
app.use(cookieParser('ilovethenodejs'))

// Get form submission data
app.use(bodyParser.text())

app.listen(8080, '127.0.0.1')
```

---

# Middleware: Custom

**Write your own middleware:**

```javascript
let app = express()


















app.listen(8080, '127.0.0.1')
```

---

# Middleware: Custom

**Write your own middleware:**

```javascript
let app = express()

// FIFO: Called 1st
app.use((req, res, next) => {



})











app.listen(8080, '127.0.0.1')
```

---

# Middleware: Custom

**Write your own middleware:**

```javascript
let app = express()

// FIFO: Called 1st
app.use((req, res, next) => {
  // If not /about, continue to next middleware


})











app.listen(8080, '127.0.0.1')
```

---

# Middleware: Custom

**Write your own middleware:**

```javascript
let app = express()

// FIFO: Called 1st
app.use((req, res, next) => {
  // If not /about, continue to next middleware
  if (req.url !== '/about') return next()

})











app.listen(8080, '127.0.0.1')
```

---

# Middleware: Custom

**Write your own middleware:**

```javascript
let app = express()

// FIFO: Called 1st
app.use((req, res, next) => {
  // If not /about, continue to next middleware
  if (req.url !== '/about') return next()
  res.end('About page')
})











app.listen(8080, '127.0.0.1')
```

---

# Middleware: Custom

**Write your own middleware:**

```javascript
let app = express()

// FIFO: Called 1st
app.use((req, res, next) => {
  // If not /about, continue to next middleware
  if (req.url !== '/about') return next()
  res.end('About page')
})

// FIFO: Called 2nd
app.use((req, res, next) => {

})






app.listen(8080, '127.0.0.1')
```

---

# Middleware: Custom

**Write your own middleware:**

```javascript
let app = express()

// FIFO: Called 1st
app.use((req, res, next) => {
  // If not /about, continue to next middleware
  if (req.url !== '/about') return next()
  res.end('About page')
})

// FIFO: Called 2nd
app.use((req, res, next) => {
  res.end('Default page')
})






app.listen(8080, '127.0.0.1')
```

---

# Middleware: Custom

**Write your own middleware:**

```javascript
let app = express()

// FIFO: Called 1st
app.use((req, res, next) => {
  // If not /about, continue to next middleware
  if (req.url !== '/about') return next()
  res.end('About page')
})

// FIFO: Called 2nd
app.use((req, res, next) => {
  res.end('Default page')
})

// FIFO: Called 3rd
app.use((req, res, next) => {

})

app.listen(8080, '127.0.0.1')
```

---

# Middleware: Custom

**Write your own middleware:**

```javascript
let app = express()

// FIFO: Called 1st
app.use((req, res, next) => {
  // If not /about, continue to next middleware
  if (req.url !== '/about') return next()
  res.end('About page')
})

// FIFO: Called 2nd
app.use((req, res, next) => {
  res.end('Default page')
})

// FIFO: Called 3rd
app.use((req, res, next) => {
  // NEVER CALLED #2 doesn't call next
})

app.listen(8080, '127.0.0.1')
```

---

# Middleware: `body-parser`

```javascript
let app = express()
let sendUser = require('./sendUser')



app.get('/user', sendUser)


.
```

---

# Middleware: `body-parser`

```javascript
let app = express()
let sendUser = require('./sendUser')
let bodyParser = require('body-parser')

app.use(bodyParser.text())
app.get('/user', sendUser)


.
```

---

# Middleware: `body-parser`

```javascript
let app = express()
let sendUser = require('./sendUser')
let bodyParser = require('body-parser')

app.use(bodyParser.text())
app.get('/user', sendUser)
app.post('/user', (req, res) => {

})
```

---

# Middleware: `body-parser`

```javascript
let app = express()
let sendUser = require('./sendUser')
let bodyParser = require('body-parser')

app.use(bodyParser.text())
app.get('/user', sendUser)
app.post('/user', (req, res) => {
  // use req.body to create new user
})
```

---

# Middleware: Basic Auth


*http://username:password@127.0.0.1:8000/user*

```javascript
let app = express()









app.get('/user', user)
```
---

# Middleware: Basic Auth

*http://username:password@127.0.0.1:8000/user*

```javascript
let app = express()
let basicAuth = require('basic-auth-connect')








app.get('/user', user)
```

---

# Middleware: Basic Auth

*http://username:password@127.0.0.1:8000/user*

```javascript
let app = express()
let basicAuth = require('basic-auth-connect')
let auth = basicAuth(validate)







app.get('/user', user)
```

---

# Middleware: Basic Auth


*http://username:password@127.0.0.1:8000/user*

```javascript
let app = express()
let basicAuth = require('basic-auth-connect')
let auth = basicAuth(validate)

let validate = (username, password, next) => {
  let result = (username === 'steve' && password === '12345')
  callback(null, result)
}


app.get('/user', user)
```

---

# Middleware: Basic Auth


*http://username:password@127.0.0.1:8000/user*

```javascript
let app = express()
let basicAuth = require('basic-auth-connect')
let auth = basicAuth(validate)

let validate = (username, password, next) => {
  let result = (username === 'steve' && password === '12345')
  next(null, result)
}


app.get('/user', user)
```

---

# Middleware: Basic Auth


*http://username:password@127.0.0.1:8000/user*

```javascript
let app = express()
let basicAuth = require('basic-auth-connect')
let auth = basicAuth(validate)

let validate = (username, password, next) => {
  let result = (username === 'steve' && password === '12345')
  next(null, result)
}

app.use(auth)
app.get('/user', user)
```

---

# Middleware: Basic Auth


*http://username:password@127.0.0.1:8000/user*

```javascript
let app = express()
let basicAuth = require('basic-auth-connect')
let auth = basicAuth(validate)

let validate = (username, password, next) => {
  let result = (username === 'steve' && password === '12345')
  next(null, result)
}


app.get('/user', auth, user)
```
---

# Express: Configuration

**Conditionally use middleware:**
```javascript
if (process.env.NODE_ENV === 'development') {
  app.use(morgan('dev')) // Verbose logging
}
```

---

# Express: Routes

```javascript
let app = express()







app.listen(8000)
```

---

# Express: Routes

```javascript
let app = express()

app.get('/version', (req, res) => {



})

app.listen(8000)
```

---

# Express: Routes

```javascript
let app = express()

app.get('/version', (req, res) => {
  res.writeHead(200, {'Content-Type': 'application/json'})
  let result = { version: '1.0.0' }
  res.end(JSON.stringify(result))
})

app.listen(8000)
```

---

# Express: Routes

```javascript
let app = express()

app.get('/version', (req, res) => {

  let result = { version: '1.0.0' }
  res.json(result)
})

app.listen(8000)
```

---

# Express: Parameters

```javascript


app.get('/user', (req, res) => {
  
  let user = { id: 1, name: 'John' }
  
  res.json(user)
})

.
```

---

# Express: Parameters

```javascript
let users = require('./users.json')

app.get('/user/:id', (req, res) => {
  
  let user = users[req.params.id]
  
  res.json(user)
})

.
```

---

# Express: Parameters

```javascript
let users = require('./users.json')

app.get('/user/:id', (req, res) => {
  
  let user = users[req.params.id]
  if (!user) return res.send(404, 'Not Found')
  res.json(user)
})

.
```

---

# Express: Parameters

```javascript
let users = require('./users.json')

app.get('/user/:id?', (req, res) => {
  if (!req.params.id) return res.json(users)
  let user = users[req.params.id]
  if (!user) return res.send(404, 'Not Found')
  res.json(user)
})

.
```

---

# Middleware: Composition

**Refactor redundant code as middleware:**

```javascript
let then = require('express-then')






app.get('/user/:id', then(async (req, res) => {
  let id = req.params.id
  let user = await User.get(id)
  res.send('user ' + user.name)
}))

app.put('/user/:id', then(async (req, res) => {
  let id = req.params.id
  let user = await User.get(id)
  user.update(req.body)
}))
```

---

# Middleware: Composition

**Refactor redundant code as middleware:**

```javascript
let then = require('express-then')
let loadUser = then(async (req, res, next) => {



})

app.get('/user/:id', then(async (req, res) => {
  let id = req.params.id
  let user = await User.get(id)
  res.send('user ' + user.name)
}))

app.put('/user/:id', then(async (req, res) => {
  let id = req.params.id
  let user = await User.get(id)
  user.update(req.body)
}))
```

---

# Middleware: Composition

**Refactor redundant code as middleware:**

```javascript
let then = require('express-then')
let loadUser = then(async (req, res, next) => {



})

app.get('/user/:id', then(async (req, res) => {


  res.send('user ' + user.name)
}))

app.put('/user/:id', then(async (req, res) => {


  user.update(req.body)
}))
```

---

# Middleware: Composition

**Refactor redundant code as middleware:**

```javascript
let then = require('express-then')
let loadUser = then(async (req, res, next) => {
  let id = req.params.id
  let user = await User.get(id)
  req.user = user
})

app.get('/user/:id', then(async (req, res) => {


  res.send('user ' + user.name)
}))

app.put('/user/:id', then(async (req, res) => {


  user.update(req.body)
}))
```

---

# Middleware: Composition

**Refactor redundant code as middleware:**

```javascript
let then = require('express-then')
let loadUser = then(async (req, res, next) => {
  let id = req.params.id
  let user = await User.get(id)
  req.user = user
})

app.get('/user/:id', then(async (req, res) => {


  res.send('user ' + user.name)
}))

app.put('/user/:id', then(async (req, res) => {


  req.user.update(req.body)
}))
```

---

# Middleware: Composition

**Refactor redundant code as middleware:**

```javascript
let then = require('express-then')
let loadUser = then(async (req, res, next) => {
  let id = req.params.id
  let user = await User.get(id)
  req.user = user
})

app.get('/user/:id', loadUser, then(async (req, res) => {


  res.send('user ' + user.name)
}))

app.put('/user/:id', loadUser, then(async (req, res) => {


  req.user.update(req.body)
}))
```

---

# Middleware: Composition

**Composable route middleware**

```javascript
app.put('/user/:id', isAdmin, loadUser, (req, res) => {
  req.user.update(req.body)
})
```

**is cleaner than...**

```javascript
app.put('/user/:id', then(async (req, res, next) => {
  await isAdmin(req, res)
  let user = await loadUser(req, res)
  user.update(req.body)
}))
```

---

# Express: Rendering Views

**Use `res.render` render view with arguments:**

```javascript
// Configure ejs view engine
app.set('views', path.join(__dirname, 'views'))
app.set('view engine', 'ejs')

// Render view
app.get('/user/:id', loadUser, (req, res) => {
  res.render('user_edit', {
    user: req.user,
    title: 'Edit User ' + req.user.username
  })
})
```

---

class: center, middle

# Questions?
