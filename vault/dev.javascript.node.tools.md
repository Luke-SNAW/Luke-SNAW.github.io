---
id: oupetc54rid9460a481qly3
title: Tools
desc: ""
updated: 1646012049967
created: 1646012035359
---

- [New in Node.js: `node:` protocol imports](https://2ality.com/2021/12/node-protocol-imports.html)
- [5 Express Middleware Libraries Every Developer Should Know](https://blog.bitsrc.io/5-express-middleware-libraries-every-developer-should-know-94e2728f7503)
- [PM2](https://pm2.keymetrics.io/): is a production process manager for Node.js applications with a built-in load balancer. It allows you to keep applications alive forever, to reload them without downtime and to facilitate common system admin tasks.
- [Development practices our NodeJS developers follow](https://www.peerbits.com/blog/development-practices-for-nodejs-developers.html)
  - Use efficient tools to restart your app
    - Nodemon: Nodemon automatically restarts the application whenever a fresh change is made to the code. You can initialize Nodemon by replacing the node with nodemon on the command line.
    - Forever: Forever provides automatic restarting along with additional configuration options. These options include writing logs and setting a working directory that would normally be printed on stdout to a file.
    - PM2: PM2 is an excellent process management tool you can use to better up your development. It allows more control and features to manage processes running in production compared to the other two. Furthermore, it ensures that the application restarts as quickly as possible in case the server it’s running on goes down.
