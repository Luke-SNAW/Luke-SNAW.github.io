
## Collections

- [New in Node.js: `node:` protocol imports](https://2ality.com/2021/12/node-protocol-imports.html)
- [5 Express Middleware Libraries Every Developer Should Know](https://blog.bitsrc.io/5-express-middleware-libraries-every-developer-should-know-94e2728f7503)
  1. Helmet — Increase HTTP Header Security
  2. Cookie-parser — Parse Cookies
  3. Passport — Access to Wide Range of Authentication Mechanisms
  4. Morgan— Log HTTP Requests and Errors
  5. CORS — Allow or Restrict Requested Resources on a Web Server
- [better-sqlite3](https://github.com/WiseLibs/better-sqlite3) - The fastest and simplest library for SQLite3 in Node.js.
- [Runtime compatibility across JavaScript runtimes](https://runtime-compat.unjs.io/)
  - https://node.green/
- [Node.js Toolbox](https://nodejstoolbox.com/) - Find actively maintained and popular libraries in the Node.js ecosystem

## CLI

- [PM2](https://pm2.keymetrics.io/) is a production process manager for Node.js applications with a built-in load balancer. It allows you to keep applications alive forever, to reload them without downtime and to facilitate common system admin tasks.
- [Development practices our NodeJS developers follow](https://www.peerbits.com/blog/development-practices-for-nodejs-developers.html)
  - Use efficient tools to restart your app
    - Nodemon: Nodemon automatically restarts the application whenever a fresh change is made to the code. You can initialize Nodemon by replacing the node with nodemon on the command line.
    - Forever: Forever provides automatic restarting along with additional configuration options. These options include writing logs and setting a working directory that would normally be printed on stdout to a file.
    - PM2: PM2 is an excellent process management tool you can use to better up your development. It allows more control and features to manage processes running in production compared to the other two. Furthermore, it ensures that the application restarts as quickly as possible in case the server it’s running on goes down.

## NPM

- [Using `npm query` for better dependency management](https://blog.logrocket.com/npm-query-better-dependency-management/)

## Validation

- [joi](https://github.com/sideway/joi) - The most powerful data validation library for JS
- [Ajv JSON schema validator](https://github.com/ajv-validator/ajv) - The fastest JSON schema Validator. Supports JSON Schema draft-04/06/07/2019-09/2020-12 and JSON Type Definition (RFC8927)
- [express-validator](https://github.com/express-validator/express-validator) - An express.js middleware for validator.js.

## Log

- [winston](https://github.com/winstonjs/winston) is designed to be a simple and universal logging library with support for multiple transports. A transport is essentially a storage device for your logs. Each winston logger can have multiple transports (see: [Transports](https://github.com/winstonjs/winston#transports)) configured at different levels (see: [Logging levels](https://github.com/winstonjs/winston#logging-levels)). For example, one may want error logs to be stored in a persistent remote location (like a database), but all logs output to the console or a local file.
- 🌲 [pino](https://github.com/pinojs/pino) - super fast, all natural json logger

## Auth

- [node-jsonwebtoken](https://github.com/auth0/node-jsonwebtoken) - JsonWebToken implementation for node.js http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html

## Framework

> https://news.ycombinator.com/item?id=33138903

There is a Laravel for Node.js - https://adonisjs.com/

+1 for Adonis. I've been using it for some time, together with unpoly + alpinejs and it's a real pleasure. I'm really productive with this stack. In fact, their docs site is built using these tools: https://github.com/adonisjs/docs.adonisjs.com/blob/develop/package.json
