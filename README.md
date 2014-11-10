connect-nedb-session
====================

**This is forked from the no-longer-maintained branch by louischatriot**

(I needed the database to clear its expired sesssions so it wouldn't grow infinitely big, so I've hacked it in.)

NeDB-backed session store for the Connect/Express session middleware.

## Install and test
```javascript
npm install connect-nedb-session
npm test
```

## How to use
```javascript
// If you use Connect alone
var connect = require('connect')
 , session = connect.session
 , NedbStore = require('connect-nedb-session')(session);

// If you use Express
var express = require('express')
 , session = express.session
 , NedbStore = require('connect-nedb-session')(session);

// If you use Express 4.x
var express = require('express')
 , session = require('express-session')
 , NedbStore = require('connect-nedb-session')(session);

// Use with the session middleware (replace express with connect if you use Connect)
server.use(session({ secret: 'yoursecret'
                   , key: 'yoursessionkey'
                   , cookie: { path: '/'
                             , httpOnly: true
                             , maxAge: 365 * 24 * 3600 * 1000   // One year for example
                             }
                   , store: new NedbStore({ filename: 'path_to_nedb_persistence_file', clearInterval: 24 * 3600 * 1000 })
                   }));
// makes a session store that clears itself every 24 hours
```

## License
MIT
